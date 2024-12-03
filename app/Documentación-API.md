
# Documentación General de la API

## Tabla de Contenidos
1. [Introducción](#introducción)
2. [Requisitos Previos](#requisitos-previos)
3. [Instalación](#instalación)
   - [Clonación del Repositorio](#clonación-del-repositorio)
   - [Configuración del Entorno](#configuración-del-entorno)
4. [Uso de Docker](#uso-de-docker)
   - [Construcción de la Imagen](#construcción-de-la-imagen)
   - [Ejecución del Contenedor](#ejecución-del-contenedor)
   - [Detener y Eliminar Contenedores](#detener-y-eliminar-contenedores)
5. [Endpoints de la API](#endpoints-de-la-api)
   - [POST /clasification_image](#post-clasification_image)
6. [Manejo de Errores](#manejo-de-errores)

---

## Introducción
Esta API permite analizar radiografías de tórax para detectar neumonía utilizando un modelo de redes neuronales convolucionales. Genera un Grad-CAM para visualizar las áreas más relevantes en las imágenes analizadas.

Es ideal para integrarse en sistemas médicos que requieran un diagnóstico automatizado complementario.

### Fecha de Actualización
Última actualización: 02-12-2024

---

## Requisitos Previos
- Docker y Docker Compose instalados.
- Git instalado.
- Python 3.12 (para desarrollo).
- Configuración básica del sistema operativo.

## Instalación

### Clonación del Repositorio
Clona el repositorio del proyecto:
```bash
git clone https://github.com/tu-usuario/proyecto-neumonia.git
cd proyecto-neumonia
```
## Carga del modelo

El modelo necesario para ejecutar la API no está incluido directamente en el repositorio debido a su tamaño. Descárgalo desde el siguiente enlace:
 
[Descargar modelo cnn_neumonía.keras](https://drive.google.com/file/d/1lIucaM2YqiQma1Z3UGR28jJuoSuR9XmT/view?usp=drive_link)

Guarda el archivo en la ubicación (/app/cnn_neumonía.keras si usas Docker).
 
## Uso de Docker

### Construcción de la Imagen
Construye la imagen de Docker:
```bash
docker build -t neumonía-api .
```

### Ejecución del Contenedor
Inicia el contenedor con Docker:
```bash
docker run -d -p 80:80 neumonía-api
```
Accede a la API en `http://localhost:80/docs` para la documentación interactiva.

### Detener y Eliminar Contenedores
Para detener un contenedor:
```bash
docker stop id_contenedor
```
Para eliminarlo:
```bash
docker rm id_contenedor
```

---

## Endpoints de la API

### POST /clasification_image
**Descripción:** Analiza una radiografía de tórax para detectar neumonía y generar un Grad-CAM.

**Request Body:**
- `file` (archivo): Archivo de imagen de la radiografía (formato JPEG o JPG).

**Ejemplo:**
```bash
curl -X POST -F "file=@radiografia.jpg" http://localhost:80/predict
```

**Response:**
```json
{
  "confidence": 0.98,
  "predicted_class": "PNEUMONIA"
}
```

---

## Manejo de Errores
La API devuelve respuestas HTTP con códigos de error estándar:
- **400**: Error en la solicitud (p. ej., imagen inválida o no soportada).
- **404**: Endpoint no encontrado.
- **500**: Error interno del servidor.

## Observaciones

- Los modelos deben estar entrenados y disponibles en el directorio `/app`.
