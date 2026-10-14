# Título Proyecto

## Miembros del grupo L3-ABS-5 (sustituir)

1. Talavera Enrique Cano, Jesús
1. Ramos Zamora, Alberto
1. Domínguez Freire, Jose Luis
1. Thomas Abello, Arve

## 1. Introducción al problema

- La empresa VeloForge nace de la pasión por el ciclismo de alto rendimiento y la ingeniería mecánica, con la ambición de convertirse en un taller de referencia en la fabricación artesanal de cuadros a medida (bespoke) y el ensamblaje de bicicletas de competición. Como taller en fase de expansión, su principal reto es competir con las grandes corporaciones industriales con producciones masivas de bajo coste, demostrando el valor diferencial de la personalización, la durabilidad y la excelencia de la fabricación a mano.
La gestión artesanal del taller requiere coordinar el abastecimiento de materiales, la asignación de carga de trabajo, y un riguroso control de tolerancias mecánicas. Por ello, es necesario desarrollar un software integral que aborde una doble necesidad estratégica: crecer de cara al público y optimizar la gestión técnica interna.


## 2. Glosario de términos

- **Alineación láser**: Procedimiento metrológico de precisión mediante el cual se comprueba en una mesa de control que las punteras y los ejes del cuadro son estrictamente coplanares (con una tolerancia inferior a 0.2 mm).
- **Artesanía ciclista**: Fabricación manual e individualizada de cuadros y componentes, empleando técnicas tradicionales de soldadura, conformado de tubos y laminado de fibras.
- **Bespoke (A medida)**: Capacidad de diseñar y construir una bicicleta adaptada de forma única a las dimensiones y a las preferencias de rendimiento del cliente.
- **Carbono Toray T800**: Tejido de fibra de carbono de alto módulo de elasticidad que ofrece una elevada rigidez estructural y ligereza tras su curado térmico controlado.
- **Cerámica (Rodamientos)**: Componentes mecánicos de baja fricción empleados en pedalieres y bujes para optimizar la eficiencia y suavidad de rodadura.
- **Cuadro**: Estructura principal o chasis de la bicicleta sobre la que se ensamblan la horquilla, ruedas, grupo de transmisión y demás componentes.
- **Diseño biomecánico**: Estudio ergonómico y cinemático del ciclista que determina las cotas exactas para maximizar la comodidad y la transferencia de potencia.
- **Garantía estructural**: Cobertura técnica ofrecida por el taller frente a roturas, defectos de soldadura o fallos de fatiga en los materiales del cuadro.
- **Geometría de catálogo**: Conjunto estandarizado de ángulos y longitudes predefinidas para fabricar cuadros bajo demanda sin requerir un estudio específico.
- **Libro de Geometrías**: Registro técnico (físico y digital) donde se archivan los planos, esquemas dimensionales y especificaciones de materiales de los diseños propios del taller.
- **Par de apriete**: Magnitud de fuerza de torsión aplicada mediante llaves para asegurar la tornillería sin dañar los componentes.
- **Punteras mecanizadas CNC**: Piezas de anclaje de las ruedas al cuadro fabricadas mediante fresado por control numérico, garantizando alta rigidez y tolerancias mínimas.
- **Racores**: Piezas de unión metálicas que abrazan los tubos del cuadro para unirlos mediante soldadura blanda o por capilaridad.
- **Restauración estructural**: Servicio técnico destinado a reparar fisuras, alinear cuadros deformados y renovar acabados de bicicletas de alto valor.
- **Soldadura TIG**: Técnica de unión manual por arco eléctrico, esencial para soldar titanio y aceros especiales sin introducir impurezas.
- **Titanio Grado 9 (Ti-3Al-2.5V)**: Aleación de titanio con 3% de aluminio y 2.5% de vanadio, referente en el sector por su ligereza, resistencia a la corrosión y capacidad de absorción de impactos.
- **Tubos conificados**: Tubería metálica cuyo grosor interno varía a lo largo del tubo para aligerar peso en el centro y mantener resistencia en las zonas de unión.
- **Wheelbuilding**: Proceso artesanal de cálculo de longitud de radios, cruces, radiado y centrado milimétrico de ruedas de competición.

## 3. Visión general del sistema

### 3.1. Requisitos generales

**Gestión del inventario**:
Es imprescindible estar al tanto de los materiales y componentes que tenemos en el almacén y reponer con facilidad aquellos que se hayan agotado o estén fuera de tolerancia. Todo ello para poder organizar los pedidos y ofrecerles a nuestros clientes bicicletas de máxima fiabilidad.

**Gestión de pedidos**:
Estar informado de las demandas de nuestros clientes con el objetivo de organizar a los constructores y montadores, y poder ofrecerle a nuestros clientes una experiencia agradable acortando los periodos de espera lo máximo posible.

**Gestión del presupuesto**:
Es de vital importancia conocer los gastos de aprovisionamiento y los beneficios en orden cronológico e informar rápidamente al gerente de los costes que manejamos en caso de desviaciones para, si es necesario, ajustar la estrategia del taller sin perder ni capital ni calidad.

**Gestión del catálogo**:
Hay que tener un registro online de los modelos, cotas de geometría y especificaciones de materiales (a excepción de los proyectos personalizados) para evitar costes innecesarios y facilitar la selección al cliente.

**Gestión de clientes**:
Hay que tener un registro de todos los clientes (ciclistas particulares y clubes) donde aparezca su información personal sumado al historial de pedidos y parámetros biomecánicos.

**Gestión de especialistas**:
Es necesario tener un registro donde aparezcan todos los artesanos y técnicos de taller, donde podremos encontrar sus datos personales, vías de contacto y sus especialidades dentro del sector.

### 3.2. Usuarios del sistema

- **Dueño**: El principal responsable del negocio (el que aporta el capital) será el estratega del taller, es decir, se encargará de elegir las líneas de producto, controlar la rentabilidad y autorizar contrataciones.
- **Cliente (Ciclistas, Clubes deportivos)**: Usuario que encarga un cuadro o bicicleta completa (sea estándar de catálogo, personalizada o un servicio técnico) al taller.
- **Constructor de Cuadros (*Framebuilder*)**: Se encarga de cortar, preparar y soldar o laminar los cuadros. Tiene contacto directo con el cliente para perfeccionar las cotas ergonómicas y asegurar que el chasis responde a sus necesidades.
- **Mecánico / Montador (*Wheelbuilder*)**: Se encarga del montaje de componentes, radiado de ruedas, guiado interno y calibración final de la bicicleta. Tiene contacto directo con el cliente para asesorarle en la selección técnica de piezas.
- **Gerente**: Se encarga de llevar el inventario del almacén, las cuentas del taller y de que el resto de empleados cumplan con las directrices del dueño. Tiene contacto directo con el cliente para concretar temas presupuestarios y de plazos.
- **Proveedor**: Empresa o distribuidor que abastece el negocio con materia prima (tubería técnica, fibras, punteras, componentes y consumibles).
- **Administrador Web**: Persona responsable de la gestión, mantenimiento y actualización de la parte pública del sitio web.


## 4. Catálogo de requisitos

### 4.1. Requisitos funcionales

**R.F.01. Consulta del Catálogo de Modelos**  
Como cliente quiero consultar el catálogo de bicicletas y el libro de geometrías, con la posibilidad de aplicar filtros por disciplina ciclista y técnica de unión para encontrar el modelo que mejor se adapte a mis necesidades e intereses.  
*Pruebas de aceptación:*
- Comprobar que el sistema muestra correctamente el catálogo completo de bicicletas y el libro de geometrías.
- Comprobar que el usuario puede filtrar los modelos seleccionando una disciplina ciclista específica.
- Comprobar que el usuario puede filtrar los modelos aplicando criterios de técnica de unión.
- Se debe aplicar la regla de negocio RN-06 para asegurar que todo modelo de catálogo esté registrado en el "Libro de Geometrías" interno con sus diagramas de cotas y especificaciones de tubería.

**R.F.02. Consulta de Perfiles de Especialistas**  
Como gerente o dueño quiero filtrar y comparar las especialidades y años de experiencia de los artesanos y mecánicos para asignar al trabajador óptimo en función de las exigencias técnicas del encargo.  
*Pruebas de aceptación:*
- Comprobar que el sistema lista correctamente a los artesanos y mecánicos del taller.
- Comprobar que se pueden filtrar según experiencia o especialidad técnica.

**R.F.03. Consulta de Ficha de Cliente**  
Como personal autorizado quiero gestionar y actualizar las preferencias y el historial de encargos de un cliente para mantener un seguimiento centralizado de su evolución técnica en el taller.  
*Pruebas de aceptación:*
- Comprobar que el sistema permite realizar búsquedas de clientes registrados por DNI o apellidos.
- Comprobar que se pueden realizar consultas filtrando por preferencias del cliente, medidas corporales o club ciclista.
- Comprobar que la ficha de cliente muestra la información personal, su historial de encargos y los parámetros o preferencias biomecánicas.

**R.F.04. Listado general de Encargos**  
Como gerente o dueño quiero consultar un listado con todos los encargos y proyectos de taller para poder filtrar por estado (Diseño/Fabricación/Montaje/Completado), cliente o especialista asignado.  
*Pruebas de aceptación:*
- Comprobar que el sistema muestra de forma global todos los encargos del taller.
- Comprobar que se pueden aplicar filtros de búsqueda por estado (Diseño, Fabricación, Montaje, Completado), por cliente o por especialista asignado.
- Se debe aplicar la regla de negocio RN-01 reflejando correctamente las restricciones de carga de trabajo y asignación en fabricación.

**R.F.05. Consulta de Encargos para el Cliente**  
Como cliente quiero consultar desde mi área personal el listado y el estado detallado del avance de mis propios encargos para estar informado sobre el proceso de fabricación o montaje.  
*Pruebas de aceptación:*
- Comprobar que el cliente, tras autenticarse, accede únicamente al listado de sus propios encargos.
- Comprobar que se detalla de forma clara el estado actual de avance de cada encargo.

**R.F.06. Consulta de Inventario de Materiales**  
Como gerente o dueño quiero gestionar alertas automáticas de stock mínimo y solicitudes de reposición para prevenir roturas de inventario en el taller de fabricación.  
*Pruebas de aceptación:*
- Comprobar que el sistema muestra el listado del inventario de materiales con su stock actual.
- Comprobar que cada material detalla su proveedor asociado, el coste unitario y su ubicación exacta en el almacén.
- Se debe aplicar la regla de negocio RN-02 para comprobar que las materias primas cumplen con los estándares de calidad y certificaciones requeridas.

**R.F.07. Consulta de Proveedores**  
Como gerente o dueño quiero gestionar la homologación y actualización de certificaciones de los proveedores para controlar qué empresas cumplen los requisitos de calidad necesarios para suministrar materias primas al taller.  
*Pruebas de aceptación:*
- Comprobar que el sistema muestra un listado completo de los proveedores dados de alta.
- Comprobar que se muestra la información de contacto, las certificaciones homologadas y el historial de pedidos de cada proveedor.
- Se debe aplicar la regla de negocio RN-02 para verificar la homologación de los proveedores de titanio y composites.

**R.F.08. Consulta de Informes Económicos**  
Como gerente o dueño quiero generar y visualizar informes sobre ventas, costes de materiales y la relación coste-beneficio de los proyectos para analizar los datos en un período determinado.  
*Pruebas de aceptación:*
- Comprobar que se calculan y visualizan correctamente las ventas, los costes de materiales y la relación coste-beneficio de los proyectos en dicho período.
- Comprobar que el sistema permite seleccionar un intervalo de fechas para la generación de informes económicos.

**R.F.09. Consulta y Seguimiento de Envíos**  
Como cliente o personal autorizado quiero consultar el estado y la información de seguimiento logístico para conocer el estado de las bicicletas o cuadros encargados.  
*Pruebas de aceptación:*
- Comprobar que el sistema permite consultar la información de seguimiento de un envío asociado a un pedido mediante su número de seguimiento o cliente.
- Comprobar que se muestra el estado logístico actual (preparando, en camino, entregado) y los datos de transporte.


#### 4.1.1. Requisitos de información

**RI-01: Modelos y Bicicletas**  
Como Framebuilder o Wheelbuilder quiero conocer toda la información acerca de los modelos que disponemos: nombre comercial, disciplina ciclista (carretera, gravel, pista), técnica de unión (soldadura TIG, racores, monocasco), los materiales empleados (titanio, fibra de carbono, acero), una descripción técnica detallada, precio base, stock disponible, fotografías y tiempo de fabricación estimado (si es bajo pedido) para conocer dichos productos.  
*Pruebas de aceptación:*
- Comprobar que el sistema registra y muestra el nombre comercial, disciplina ciclista (carretera, gravel, pista) y técnica de unión (soldadura TIG, racores, monocasco) de cada modelo.
- Comprobar que se detallan los materiales empleados (titanio, fibra de carbono, acero), la descripción técnica, el precio base, el stock disponible y las fotografías.
- Comprobar que el sistema muestra el tiempo de fabricación estimado para los modelos bajo pedido.
- Se debe aplicar la regla de negocio RN-06 para verificar que todo modelo de catálogo está vinculado al Libro de Geometrías.

**RI-02: Especialistas**  
Como gerente o dueño quiero conocer a nuestros artesanos y mecánicos: nombre completo, especialidad técnica, una breve biografía, años de experiencia en el sector y una foto de perfil para conocer a nuestros trabajadores.  
*Pruebas de aceptación:*
- Comprobar que el sistema almacena y muestra el nombre completo y la especialidad técnica de cada artesano y mecánico.
- Comprobar que se visualizan la biografía, la foto de perfil y los años de experiencia en el sector de cada trabajador.
- Se debe aplicar la regla de negocio RN-07 para validar que los especialistas registrados cumplen con el requisito mínimo de experiencia exigido.

**RI-03: Contratación**  
Como dueño quiero conocer a varios especialistas y contratarlos en el caso de que fueran de ayuda en el negocio: nombre completo, DNI, edad, localidad, años de experiencia en el sector, especialidad, qué pueden aportar al taller, email y teléfono de contacto para conocer profesionales y contratar los servicios de aquellos que mejor concuerden con la empresa.  
*Pruebas de aceptación:*
- Comprobar que el sistema permite registrar los datos personales de candidatos (nombre completo, DNI, edad, localidad, email y teléfono).
- Comprobar que se recogen los años de experiencia, especialidad y lo que el candidato puede aportar al taller.
- Se debe aplicar la regla de negocio RN-07 para que el sistema rechace automáticamente la contratación o alta si el candidato no cuenta con al menos 3 años de experiencia acreditada.

**RI-04: Clientes y Especificaciones Biomecánicas**  
Como gerente de la empresa quiero disponer de la información correspondiente a los clientes: nombre y apellidos, localidad, DNI, datos de contacto (número de teléfono, correo electrónico), club o federación a la que pertenece y preferencias ergonómicas (material preferido, presupuesto, especialista de preferencia, etc.) para tener control sobre los clientes.  

Como constructor o montador quiero contactar directamente con los clientes para que me den sus especificaciones biomecánicas y, si es necesario, aconsejarlos para poder buscar la geometría óptima acorde a lo que el ciclista solicite.  
*Pruebas de aceptación:*
- Comprobar que el sistema almacena y muestra los datos personales, de contacto y federativos de cada cliente.
- Comprobar que se registran las preferencias de materiales, presupuesto y especialista predilecto.
- Comprobar que los artesanos y mecánicos pueden consultar directamente las especificaciones ergonómicas y medidas biomecánicas asociadas a la ficha del cliente.

**RI-05: Encargos Especiales y Proyectos**  
Como gerente de la empresa quiero tener toda la información posible en cuanto a los proyectos: nº de encargo y del cliente, especialista que lo realizó, presupuesto acordado por el cliente, fecha de entrega estimada y estado del proceso (Diseño/Fabricación/Montaje/Completado) para poder informar a nuestro cliente con todo lo que necesite.  
*Pruebas de aceptación:*
- Comprobar que el sistema genera y visualiza el código identificador del proyecto, cliente vinculado, especialista asignado, presupuesto cerrado y fecha estimada de entrega.
- Comprobar que el encargo avanza ordenadamente por sus estados (Diseño, Fabricación, Montaje, Completado).
- Se debe aplicar la regla de negocio RN-01 para verificar que el especialista no supere el límite máximo de 3 proyectos simultáneos en taller.
- Se debe aplicar la regla de negocio RN-03 para verificar que el encargo no pase a estado final sin el checklist de control de calidad superado.

**RI-06: Materiales e Inventario**  
Como gerente de la empresa quiero saber todo sobre nuestro inventario: materiales, proveedor principal y secundario, norma de calidad, stock actual y mínimo, coste de la unidad, ubicación en el taller y sus certificados técnicos para resolver dudas, calcular presupuestos y planificar compras.  
*Pruebas de aceptación:*
- Comprobar que el sistema lista las materias primas con su stock disponible, stock de seguridad, coste por unidad y ubicación física en almacén (pasillo/estante/gaveta).
- Comprobar que cada material referencia a sus proveedores habituales (principal y secundario).
- Se debe aplicar la regla de negocio RN-02 para comprobar que los materiales críticos (titanio Grado 9 y fibra ISO 4210) tienen asociado su

#### 4.1.2. Reglas de negocio

- **RN-01: Límite de carga de trabajo en banco**  
  Como gerente de la empresa, quiero que se lleve un seguimiento del número de proyectos que se están llevando a cabo por cada especialista, ya que cada uno tiene un límite máximo de 3 encargos que pueden tener asignados en fabricación de forma simultánea, para que se tenga en cuenta la imposibilidad de asignar un especialista que tenga el cupo máximo alcanzado.

- **RN-02: Calidad y Certificación del Material**  
  Como gerente de la empresa, quiero que, al comprar la materia prima, se asegure que la tubería de titanio sea de aleación Grado 9 o superior y que los composites de carbono cumplan con la norma ISO 4210 con un certificado técnico para poder proporcionar un producto seguro y duradero a nuestra clientela.

- **RN-03: Control de Calidad Integral**  
  Como gerente de la empresa, quiero asegurarme de que, antes de entregar una bicicleta o cuadro, ésta haya pasado por una inspección final que verifique: alineación láser de punteras (<0.2 mm), apriete dinamométrico certificado y la ausencia total de defectos superficiales.

- **RN-04: Garantía Estructural "VeloForge"**  
  Como gerente de la empresa, me encargaré de que, si un usuario sufre daños estructurales en un cuadro, este tenga en rigor la garantía de 3 años que se ofrece contra defectos de fabricación o rotura de soldadura, para así proporcionar orden y respaldo dentro de la empresa.

- **RN-05: Política de Devoluciones y Proyectos Personalizados**  
  Como gerente de la empresa, me encargaré de que, si se realiza alguna devolución de un producto estándar, esta esté dentro del plazo máximo de 14 días desde la entrega, excluyendo de dicha posibilidad a todos los cuadros o montajes catalogados como personalizados a medida.

- **RN-06: Libro de Geometrías Registrado**  
  Como gerente de la empresa, quiero que todo modelo de catálogo esté registrado en un "Libro de Geometrías" interno (físico y digital) con sus diagramas de cotas y especificaciones de tubería (a excepción de los proyectos biomecánicos a medida).

- **RN-07: Experiencia de los nuevos especialistas**  
  Como gerente de la empresa, quiero que, al contratar un nuevo artesano o mecánico de taller, este deba tener al menos 3 años de experiencia acreditada en el sector.


### 4.2. Mapa de historias de usuario (opcional)

### 4.2. Requisitos no funcionales (opcional)

- **RNF-001: Seguridad**  
  Como encargado de la empresa, quiero que los pagos telemáticos cumplan con el protocolo de seguridad PCI-DSS y cifrado TLS 1.3 a la hora de abonar señales y facturas, para así proteger los datos bancarios y transmitir seguridad al cliente.

- **RNF-002: Utilidad y Usabilidad**  
  Como encargado de la empresa, quiero que la interfaz de visualización de cotas y fichas técnicas sea clara, legible e intuitiva para usuarios de cualquier nivel técnico, tanto en pantallas de taller como en ordenadores personales.

- **RNF-003: Compatibilidad**  
  Como encargado de la empresa, quiero que la plataforma funcione correctamente en iOS, Android y los principales navegadores web del mercado (Chrome, Firefox, Safari, Edge) para facilitar el acceso desde cualquier dispositivo.

- **RNF-004: Disponibilidad 24/7**  
  Como gerente de la empresa, quiero que la disponibilidad del portal web y del área de seguimiento sea lo más cercana posible al 99.5% anual (24 horas al día, 7 días a la semana) para facilitar las consultas y dar flexibilidad horaria a los clientes.

-- fin entregable 1 --

## 5. Modelo conceptual

### 5.1. Diagramas de clases UML

- con restricciones.

### 5.2. Escenarios de prueba

- con descripción textual y diagrama de objetos UML.

## 6. Matrices de trazabilidad

- Matriz de trazabilidad entre los elementos del modelo conceptual y los requisitos.

|       | EntidadX   | AsociaciónX  | RestricciónX  | Entidad2 ...   | 
|:------|:-----------|:-----------|:-----------|:-----------|
| RI-1  | X          | X          | X          | X          |
| RI-2  |            | X          |            | X          |
| RF-1  |            | X          |            | X          |
| RF-2  | X          |            | X          | X          |
| RN-1  |            | X          |            |            |
| RN-2  | X          | X          | X          |            |
| ...   |            |            |            |            |

-- fin entregable 2 --

## 7. Modelo relacional en 3FN

- Relaciones obtenidas al aplicar la transformación del modelo conceptual.

### 7.1.  Justificación de la estrategia de transformación de jerarquías

- si se identificaron jerarquías en el MC.


### 8. Matriz de trazabilidad MC/SQL (opcional):

- Restricciones sobre el MC / Elementos del modelo tecnológico (SQL) (Triggers, checks, etc.)
- Incluir Reglas de negocio — Constraints/Triggers en las matrices de trazabilidad para el entregable 3

|       | EntidadX   | AsociaciónX  | RestricciónX  | Entidad2 ...   | 
|:-------|:-------|:-------|:-------|:-------|
| TABLA-1 |        |        |        |        |
| TABLA-2 |        |        |        |        |
| TABLA-3 |        |        |        |        |
| TABLA-4 |        |        |        |        |
| TRIG-1 |        |        |        |        |
| TRIG-2 | X      | X      |        | X      |
| TRIG-3 |        | X      |        | X      |
| TRIG-4 |        |        | X      |        |
| CONST-1 |        |        |        |        |
| CONST-2 | X      | X      |        | X      |
| CONST-3 |        | X      |        | X      |
| CONST-4 |        |        | X      |        |

Se consideran todo tipo de constraints declarativas (aquellas definidas durante el CREATE TABLE).
-- fin entregable 3 --

## Referencias


