# OpenHIS-UNLaM

Prototipo académico de un Sistema de Información Hospitalaria para el Hospital Universitario San Justo, desarrollado en la materia **Informática Biomédica y Tecnologías de la Salud** de la Universidad Nacional de La Matanza (UNLaM).

## Objetivo

Integrar la gestión administrativa y clínica de pacientes, profesionales, intervenciones y turnos médicos mediante una base de datos centralizada, incorporando mecanismos de seguridad, trazabilidad e interoperabilidad.

## Equipo y metodología

El desarrollo se organizó mediante Scrum, en diez sprints y 23 historias de usuario. Responsables según la bitácora final:

| Integrante | Historias de usuario |
|---|---|
| Víctor | HU 01–06 |
| Lautaro | HU 07–10 |
| Micaela | HU 11–18 |
| Kevin | HU 19–23 |

Link a la plantilla de Scrum: https://ingunlamedu-my.sharepoint.com/:x:/g/personal/ldasilva_alumno_unlam_edu_ar/cQpb2zuD-pN_TpS67ce14WlFEgUD3T_p_nrVCCVivqefNgFAeQ

## Funcionalidades

- Gestión de pacientes y profesionales, altas, búsquedas, modificaciones y bajas lógicas.
- Tablas maestras: especialidades, SNOMED CT, fármacos y catálogo de obras sociales.
- Registro de signos vitales, prescripciones y consulta de intervenciones.
- Autenticación, roles y auditoría.
- Importación y exportación de recursos HL7 FHIR en JSON; generación de recetas XML y reportes HTML.
- Conversión, anonimización y visualización de imágenes DICOM.
- Agenda profesional, disponibilidad, gestión de turnos, asignación sugerida, cola de recordatorios y asistencia.
- Historia Clínica Electrónica: consultas, evolución, línea de tiempo, antecedentes y auditoría.

## Tecnologías y requisitos

- Python 3 (el equipo utiliza Python 3.13).
- Tkinter / ttk y SQLite (biblioteca estándar de Python).
- Pillow, NumPy y pydicom para el módulo de imágenes médicas.
- DB Browser for SQLite (opcional, para inspeccionar la base de datos).

## Instalación y ejecución

1. Descargar o clonar el repositorio y abrir una terminal en su carpeta raíz.
2. Instalar las dependencias de imágenes:

   ```bash
   python -m pip install pillow numpy pydicom
   ```

3. Verificar que exista `BD/Salud.db`. Conservar una copia de seguridad antes de realizar pruebas.
4. Iniciar el menú principal (versión actual utilizada para la demo):

   ```bash
   python _Menu_principal_app.pyw
   ```

   Si la copia del repositorio utiliza `_Menu.pyw` como punto de entrada, ejecutar ese archivo en su lugar. Verificar que el menú incluya Agenda profesional.
5. Iniciar sesión con un usuario de prueba habilitado. Los módulos visibles dependen del rol.

## Arquitectura

Aplicación de escritorio modular en Python. El menú inicia los módulos como procesos independientes, que comparten la base SQLite y el mecanismo de sesión y auditoría.

| Archivo | Funcionalidad |
|---|---|
| `_Menu_principal_app.pyw` / `_Menu.pyw` | Login y menú según roles |
| `_Pacientes_def_app.pyw` | Pacientes |
| `_Profesionales_def_app.pyw` | Profesionales |
| `_Tablas_maestras.pyw` | Catálogos |
| `_Signos_vitales_def_app.pyw` | Signos vitales |
| `_Prescripciones_def_app.pyw` | Prescripciones y recetas |
| `_Usuarios_app.pyw` | Usuarios y roles |
| `Auditoria_utiles.py` | Sesión y auditoría |
| `_Consulta_intervenciones.pyw` | Consulta clínica |
| `_Interoperabilidad_FHIR.pyw` | Intercambio FHIR |
| `_Herramientas_DICOM_Visor.pyw` | Imágenes DICOM |
| `_Agenda_profesionales.pyw` | Agenda y disponibilidad |
| `_Gestion_turnos.pyw` | Gestión de turnos |
| `_Asignacion_recordatorios.pyw` | Asignación, recordatorios y asistencia |
| `_HCE.pyw` | Historia Clínica Electrónica |
| `BD/Salud.db` | Base de datos |

## Alcance y limitaciones

Proyecto educativo, no destinado a uso asistencial real. Los recordatorios se generan en una cola; no se envían SMS reales. Las solicitudes por teléfono y WhatsApp se registran manualmente, sin integración con la API de WhatsApp Business. El intercambio FHIR implementa un subconjunto de recursos y no acredita conformidad integral. Los archivos DICOM generados a partir de JPG/PNG no equivalen a estudios originales. El mecanismo de seguridad del prototipo requiere refuerzo para producción.

Utilizar únicamente datos ficticios o debidamente desidentificados. No publicar credenciales, archivos de sesión `.sesion` ni bases con datos reales. Las funcionalidades deben verificarse en la versión instalada antes de la demostración.
