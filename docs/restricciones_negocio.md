# Reglas de negocio (RN-01 a RN-07)

Este documento explica en lenguaje natural las reglas de negocio de VeloForge y cómo se reflejan en el modelo conceptual (`modelo_conceptual.drawio`). 



## RN-01 · Límite de carga de trabajo en banco

**Qué dice:** un especialista no puede tener más de **3 encargos simultáneos en fabricación activa**. Si ya tiene 3, el sistema bloquea una nueva asignación y avisa al gerente de que ese especialista no está disponible.

**Por qué:** evitar la sobrecarga y proteger la precisión del trabajo artesanal.

**En el modelo:** se cuentan los encargos del especialista cuyo `estado` es `Fabricación` o `Diseño`. Las fases de preparación, corte y soldadura se consideran incluidas en el estado `Fabricación`.


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


---

## RN-03 · Control de calidad integral

**Qué dice:** antes de entregar una bicicleta o un cuadro, debe superar una **inspección final obligatoria** con tres comprobaciones:

1. Alineación láser de punteras **inferior a 0,2 mm**.
2. Apriete dinamométrico certificado.
3. Ausencia de defectos superficiales.

Un encargo no puede pasar a `Completado` ni a `Listo para Entrega` si alguno de estos puntos no está validado. Si el checklist falla, el encargo pasa automáticamente a `En Revisión de Banco`.

**Por qué:** que ninguna bicicleta salga del taller sin inspección completa.

**En el modelo:** el checklist es `ChecklistCalidad` (`alineacionLaserMm`, `paresAprieteValidados`, `sinDefectosSuperficiales`), asociado a `Encargo`. El valor de alineación debe ser estrictamente menor que 0,2 mm. El paso automático a `En Revisión de Banco` es un comportamiento del sistema, no una condición del modelo.

---

## RN-04 · Garantía estructural «VeloForge»

**Qué dice:** toda venta formalizada incluye una **garantía estructural de 3 años** contra defectos de fabricación o fallos de soldadura. La caducidad se calcula automáticamente **desde la fecha de expedición de la factura** (fecha de factura + 3 años naturales) y la garantía queda vinculada al **número de serie/bastidor** del cuadro.

**En el modelo:** `Encargo` incorpora `fechaFactura` y `numeroSerieBastidor`. La fecha de caducidad (`fechaCaducidadGarantia`) se calcula al generar la factura.

---

## RN-05 · Devoluciones y proyectos personalizados

**Qué dice:** el derecho de desistimiento de **14 días naturales** solo se aplica a **productos estándar de catálogo**. Quedan excluidos los cuadros o bicicletas fabricados a medida según especificaciones biomecánicas del cliente.

**En el modelo:** al tramitar una devolución, el sistema comprueba `esPersonalizado`. Si es `true`, la deniega e informa de la exclusión. Si es `false`, comprueba que la solicitud llega como máximo 14 días naturales después de `fechaEntregaReal`, que es un atributo nuevo en `Encargo`.


---

## RN-06 · Libro de Geometrías registrado

**Qué dice:** todo modelo estándar de catálogo debe estar registrado en el **Libro de Geometrías** interno, con sus cotas de fabricación (*stack*, *reach*, ángulos). Los proyectos personalizados quedan exentos y pueden introducir sus cotas ergonómicas directamente.

**En el modelo:** un encargo no personalizado exige que su `Modelo` tenga un `LibroGeometria` asociado y **activo** (atributo nuevo `activo`). En los personalizados, las cotas se guardan en `cotasAjustadas`.


---

## RN-07 · Experiencia de los nuevos especialistas

**Qué dice:** al dar de alta un especialista de taller, debe acreditar **al menos 3 años de experiencia** en el sector artesanal. Si el valor es menor, el alta se rechaza y se informa del incumplimiento.

**En el modelo:** se valida el atributo `anosExperiencia` de `Especialista`.


---


