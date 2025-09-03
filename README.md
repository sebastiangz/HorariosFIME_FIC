# Generador de Listas de Asistencia FIC

## Descripción

`genera_listas_FIC_fet.py` es una herramienta desarrollada para generar automáticamente listas de asistencia docente a partir de horarios escolares exportados desde FET (Free Timetabling Software). El sistema está diseñado para optimizar el proceso administrativo consolidando clases consecutivas del mismo profesor con el mismo grupo, requiriendo una sola firma por bloque de clases.

## Características Principales

- **Procesamiento de XML de FET**: Extrae información completa de horarios, profesores, materias y grupos
- **Consolidación Inteligente**: Detecta y consolida automáticamente clases consecutivas del mismo profesor con el mismo grupo
- **Flexibilidad de Horarios**: Adapta diferentes formatos de horario por plantel (07:00-08:00, 07:00-07:50, etc.)
- **Múltiples Formatos de Salida**: Genera archivos en formato texto plano (.txt) y Excel (.xlsx)
- **Sección de Firmas Integrada**: Incluye automáticamente tablas de firma por día
- **Nombres Completos**: Preserva los nombres completos de las materias sin simplificaciones
- **Reportes Adicionales**: Genera resúmenes por profesor y estadísticas del horario

## Requisitos del Sistema

### Software Requerido
- Python 3.7 o superior
- Acceso a archivos XML generados por FET

### Dependencias Python
```
pandas>=1.3.0
openpyxl>=3.0.0
```

## Instalación

1. Clone o descargue el repositorio:
```bash
git clone [URL_DEL_REPOSITORIO]
cd [NOMBRE_DEL_DIRECTORIO]
```

2. Instale las dependencias:
```bash
pip install -r requirements.txt
```

O manualmente:
```bash
pip install pandas openpyxl
```

3. Verifique la instalación ejecutando:
```bash
python genera_listas_FIC_fet.py --help
```

## Uso

### Ejecución Básica

```bash
python genera_listas_FIC_fet.py
```
https://raw.githubusercontent.com/sebastiangz/HorariosFIME_FIC/main/_info/uso.jpg

El programa solicitará interactivamente:
1. Ruta del archivo XML de FET
2. Carpeta de salida (opcional, por defecto: `listas_asistencia`)
3. Opciones adicionales (resumen por profesores, estadísticas)

### Ejemplo de Uso

```
=== GENERADOR DE LISTAS DE ASISTENCIA FIC DESDE XML DE FET ===

Ingrese la ruta del archivo XML de FET: horario_agosto_2025.xml

Procesando archivo XML...
Consolidando clases consecutivas del mismo profesor...
Procesadas clases de 5 días

Carpeta de salida (Enter para 'listas_asistencia'): 

Generando listas de asistencia...
Lista de asistencia generada para Lunes: Lista_Asistencia_Lunes_20250902
Lista de asistencia generada para Martes: Lista_Asistencia_Martes_20250902
...

¿Generar resumen por profesores? (s/n): s
¿Generar estadísticas del horario? (s/n): s

¡Proceso completado exitosamente!
```

## Estructura de Archivos Generados

```
listas_asistencia/
├── Lista_Asistencia_Lunes_YYYYMMDD.txt
├── Lista_Asistencia_Lunes_YYYYMMDD.xlsx
├── Lista_Asistencia_Martes_YYYYMMDD.txt
├── Lista_Asistencia_Martes_YYYYMMDD.xlsx
├── ...
├── resumen_profesores.txt (opcional)
└── estadisticas_horario.txt (opcional)
```

### Formato de Listas de Asistencia

Cada archivo incluye:
- **Encabezado**: Día y fecha de generación
- **Bloques de Horario**: Agrupados por rangos de tiempo
- **Información por Clase**: Número de trabajador, nombre del profesor, grupo, materia, horario específico
- **Sección de Firmas**: Tabla de dos columnas con espacios para firmas de todos los profesores del día

### Ejemplo de Salida

```
LISTAS DE ASISTENCIA - LUNES
Fecha de generación: 02/09/2025
====================================================================================================

**HORARIO: 07:00 - 10:00**

NUM.     NOMBRE                    GRUPO    MATERIA                              HORARIO              TEMA     FIRMA    OBSERVACIONES
TRAB.    
------------------------------------------------------------------------------------------------------------------------
5008     Álvarez Lugo Ana Lucía    1G       EXPRESIÓN ORAL Y ESCRITA            07:50 - 08:40                          
6109     Cortes Lugo Hugo          1A       FÍSICA EXPERIMENTAL                 07:00 - 09:00                          

================================================================================
FIRMAS
================================================================================

___________________________________    ___________________________________
PROFESOR                               PROFESOR
-----------------------------------    -----------------------------------
5008 - Álvarez Lugo Ana Lucía         6109 - Cortes Lugo Hugo
___________________________________    ___________________________________
```

## Funcionalidades Técnicas

### Consolidación de Clases Consecutivas

El sistema detecta automáticamente cuando un profesor tiene horas consecutivas con el mismo grupo y las consolida en un solo registro:

**Antes de la consolidación**:
- 07:00-08:00: Profesor A, Grupo 1A, Matemáticas
- 08:00-09:00: Profesor A, Grupo 1A, Matemáticas

**Después de la consolidación**:
- 07:00-09:00: Profesor A, Grupo 1A, Matemáticas

### Manejo de Materias Múltiples

Cuando un profesor tiene clases consecutivas de diferentes materias con el mismo grupo, se combinan:
- Resultado: "MATEMÁTICAS I / FÍSICA GENERAL"

## Configuración y Personalización

### Horarios Flexibles
El programa detecta automáticamente el formato de horarios usado por cada plantel:
- Formato estándar: "07:00-08:00"
- Formato con espacios: "07:00 - 08:00"
- Horarios de 50 minutos: "07:00-07:50"

### Bloques de Horario
Los bloques se generan automáticamente basándose en los horarios detectados, agrupando períodos relacionados para mejor legibilidad.

## Resolución de Problemas

### Errores Comunes

1. **Error: El archivo XML no existe**
   - Verifique que la ruta del archivo sea correcta
   - Asegúrese de que el archivo tenga extensión .xml

2. **Error al procesar el archivo XML**
   - Confirme que el archivo fue exportado correctamente desde FET
   - Verifique que el archivo no esté corrupto

3. **No se encontraron horarios**
   - Verifique que el archivo XML contenga información de horarios
   - Asegúrese de que los días estén en español (Lunes, Martes, etc.)

### Logs y Depuración

El programa muestra información detallada durante la ejecución:
- Número de días procesados
- Cantidad de clases consolidadas
- Archivos generados exitosamente

## Limitaciones

- Solo procesa archivos XML generados por FET
- Los días deben estar nombrados en español
- Requiere que los profesores tengan formato "NOMBRE - NUMERO" para extraer números de trabajador

## Licencia y Uso

Este software es de uso privado y no está disponible bajo licencia open source. El uso está restringido según los términos establecidos por el propietario.

## Contacto y Soporte

Para soporte técnico o consultas sobre el sistema, contacte al desarrollador a través de los canales oficiales de la institución.

## Historial de Versiones

### Versión Actual
- Consolidación automática de clases consecutivas
- Soporte para múltiples formatos de horario
- Generación de archivos Excel y texto
- Sección de firmas integrada
- Reportes adicionales opcionales

---

**Nota**: Este README proporciona información para el uso del sistema. Para modificaciones o personalizaciones adicionales, consulte con el desarrollador.
