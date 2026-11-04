# Reglas de negocio (RN-01 a RN-07)

Este documento explica en lenguaje natural las reglas de negocio de VeloForge y cómo se reflejan en el modelo conceptual (`modelo_conceptual.drawio`). Cada regla incluye su explicación, los elementos del modelo que intervienen, su expresión formal (OCL) y los criterios de aceptación.

## Resumen

| Regla | Tema | Clases implicadas |
|-------|------|-------------------|
| RN-01 | Máximo de 3 encargos simultáneos por especialista | `Especialista`, `Encargo` |
| RN-02 | Material crítico homologado y certificado | `Material`, `Proveedor`, `PedidoMaterial`, `ConsumoMaterial` |
| RN-03 | Control de calidad obligatorio antes de entregar | `Encargo`, `ChecklistCalidad` |
| RN-04 | Garantía estructural de 3 años desde la factura | `Encargo` |
| RN-05 | Devoluciones solo en productos estándar, en 14 días | `Encargo` |
| RN-06 | Modelos estándar con Libro de Geometrías activo | `Encargo`, `Modelo`, `LibroGeometria` |
| RN-07 | Mínimo 3 años de experiencia para ser especialista | `Especialista` |

---

## RN-01 · Límite de carga de trabajo en banco

**Qué dice:** un especialista no puede tener más de **3 encargos simultáneos en fabricación activa**. Si ya tiene 3, el sistema bloquea una nueva asignación y avisa al gerente de que ese especialista no está disponible.

**Por qué:** evitar la sobrecarga y proteger la precisión del trabajo artesanal.

**En el modelo:** se cuentan los encargos del especialista cuyo `estado` es `Fabricación` o `Diseño`. Las fases de preparación, corte y soldadura se consideran incluidas en el estado `Fabricación`.

```ocl
Especialista.encargos->select(e | e.estado = 'Fabricación' or e.estado = 'Diseño')->size() <= 3
```

**Criterios de aceptación**
- Se registra el recuento de proyectos activos por especialista.
- Con 3 encargos activos, se bloquea una nueva asignación y se notifica al gerente.

---

## RN-02 · Calidad y certificación del material

**Qué dice:** el material crítico debe estar certificado y proceder de un proveedor homologado:

- La tubería técnica debe acreditar aleación de **Titanio Grado 9 o superior**.
- Los composites de carbono deben tener certificación según la **norma ISO 4210**.
- No se pueden usar lotes no homologados.

Esto se traduce en dos condiciones:

1. **Entrada en almacén (RN-02a):** el material crítico solo puede entrar a través de un pedido a un proveedor homologado.
2. **Uso en taller (RN-02b):** antes de consumir material crítico hay que marcar la conformidad de su certificado técnico.

**En el modelo:** `Material` incorpora `esCritico` (tubería técnica y composites) y `certificadoConforme` (conformidad del certificado verificada). La acreditación concreta (Titanio Grado 9, ISO 4210) se registra en `especificacionTecnica` y `certificadoCalidad`. La certificación se controla **por material**, no por lote.

```ocl
-- RN-02a
context PedidoMaterial
inv: self.lineas->forAll(l | l.material.esCritico implies self.proveedor.esHomologado)

-- RN-02b
context ConsumoMaterial
inv: self.material.esCritico implies self.material.certificadoConforme = true
```

**Criterios de aceptación**
- Toda entrada de material crítico en almacén se vincula a un proveedor homologado.
- El sistema exige marcar la conformidad del certificado antes de habilitar el material para su consumo.

---

## RN-03 · Control de calidad integral

**Qué dice:** antes de entregar una bicicleta o un cuadro, debe superar una **inspección final obligatoria** con tres comprobaciones:

1. Alineación láser de punteras **inferior a 0,2 mm**.
2. Apriete dinamométrico certificado.
3. Ausencia de defectos superficiales.

Un encargo no puede pasar a `Completado` ni a `Listo para Entrega` si alguno de estos puntos no está validado. Si el checklist falla, el encargo pasa automáticamente a `En Revisión de Banco`.

**Por qué:** que ninguna bicicleta salga del taller sin inspección completa.

**En el modelo:** el checklist es `ChecklistCalidad` (`alineacionLaserMm`, `paresAprieteValidados`, `sinDefectosSuperficiales`), asociado a `Encargo`. El valor de alineación debe ser estrictamente menor que 0,2 mm. El paso automático a `En Revisión de Banco` es un comportamiento del sistema, no una condición del modelo.

```ocl
(self.estado = 'Completado' or self.estado = 'Listo para Entrega') implies
  (self.controlCalidadSuperado = true and
   self.checklistCalidad.alineacionLaserMm < 0.2 and
   self.checklistCalidad.paresAprieteValidados = true and
   self.checklistCalidad.sinDefectosSuperficiales = true)
```

**Criterios de aceptación**
- Existe un checklist técnico con los tres puntos obligatorios.
- El sistema impide cambiar el estado a `Completado` o `Listo para Entrega` si algún ítem no está validado.
- Ante un fallo, el encargo pasa a `En Revisión de Banco`.

---

## RN-04 · Garantía estructural «VeloForge»

**Qué dice:** toda venta formalizada incluye una **garantía estructural de 3 años** contra defectos de fabricación o fallos de soldadura. La caducidad se calcula automáticamente **desde la fecha de expedición de la factura** (fecha de factura + 3 años naturales) y la garantía queda vinculada al **número de serie/bastidor** del cuadro.

**En el modelo:** `Encargo` incorpora `fechaFactura` y `numeroSerieBastidor`. La fecha de caducidad (`fechaCaducidadGarantia`) se calcula al generar la factura.

```ocl
self.fechaFactura <> null implies
  (self.fechaCaducidadGarantia = self.fechaFactura + 3 años and
   self.numeroSerieBastidor <> null)
```

**Criterios de aceptación**
- Al generar la factura, el sistema calcula automáticamente la fecha límite de garantía.
- La garantía queda registrada y vinculada al número de serie/bastidor.

---

## RN-05 · Devoluciones y proyectos personalizados

**Qué dice:** el derecho de desistimiento de **14 días naturales** solo se aplica a **productos estándar de catálogo**. Quedan excluidos los cuadros o bicicletas fabricados a medida según especificaciones biomecánicas del cliente.

**En el modelo:** al tramitar una devolución, el sistema comprueba `esPersonalizado`. Si es `true`, la deniega e informa de la exclusión. Si es `false`, comprueba que la solicitud llega como máximo 14 días naturales después de `fechaEntregaReal`, que es un atributo nuevo en `Encargo`.

```ocl
self.devolucionSolicitada implies
  (not self.esPersonalizado and
   fechaSolicitud - self.fechaEntregaReal <= 14 días naturales)
```

**Criterios de aceptación**
- Al tramitar una devolución, se comprueba `esPersonalizado`.
- Si el encargo es personalizado, se deniega automáticamente.
- Si es estándar, se valida el plazo de 14 días naturales desde la entrega.

---

## RN-06 · Libro de Geometrías registrado

**Qué dice:** todo modelo estándar de catálogo debe estar registrado en el **Libro de Geometrías** interno, con sus cotas de fabricación (*stack*, *reach*, ángulos). Los proyectos personalizados quedan exentos y pueden introducir sus cotas ergonómicas directamente.

**En el modelo:** un encargo no personalizado exige que su `Modelo` tenga un `LibroGeometria` asociado y **activo** (atributo nuevo `activo`). En los personalizados, las cotas se guardan en `cotasAjustadas`.

```ocl
not self.esPersonalizado implies
  (self.modelo.libroGeometria <> null and
   self.modelo.libroGeometria.activo = true)
```

**Criterios de aceptación**
- Todo modelo no personalizado tiene asociada una ficha activa del Libro de Geometrías.
- Los encargos personalizados admiten cotas a medida sin depender del libro.

---

## RN-07 · Experiencia de los nuevos especialistas

**Qué dice:** al dar de alta un especialista de taller, debe acreditar **al menos 3 años de experiencia** en el sector artesanal. Si el valor es menor, el alta se rechaza y se informa del incumplimiento.

**En el modelo:** se valida el atributo `anosExperiencia` de `Especialista`.

```ocl
self.anosExperiencia >= 3
```

**Criterios de aceptación**
- Al tramitar el alta, el sistema valida que `anosExperiencia` sea igual o superior a 3.
- Si es menor, rechaza el alta e informa del requisito.

---

## Cambios introducidos en el modelo

| Clase | Atributo nuevo | Regla |
|-------|----------------|-------|
| `Material` | `esCritico: Boolean` | RN-02 |
| `Material` | `certificadoConforme: Boolean` | RN-02 |
| `Encargo` | `fechaFactura: Date` | RN-04 |
| `Encargo` | `numeroSerieBastidor: String` | RN-04 |
| `Encargo` | `fechaEntregaReal: Date` | RN-05 |
| `LibroGeometria` | `activo: Boolean` | RN-06 |
