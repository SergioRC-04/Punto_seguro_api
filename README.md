# 🌩️ Punto Seguro — API

> API REST en Django que provee datos climáticos, geoespaciales y de predicción para la plataforma de preparación ante emergencias **Punto Seguro**.

[![Django](https://img.shields.io/badge/Django-5.1-092E20?style=flat-square&logo=django)]()
[![DRF](https://img.shields.io/badge/Django%20REST%20Framework-3.15-red?style=flat-square)]()
[![DB](https://img.shields.io/badge/PostgreSQL-Aiven-336791?style=flat-square&logo=postgresql)]()
[![ML](https://img.shields.io/badge/scikit--learn-Predicción%20Climática-F7931E?style=flat-square&logo=scikitlearn)]()

🏆 Parte del proyecto **Punto Seguro**, registrado oficialmente en el portal de [Datos Abiertos de Colombia](https://herramientas.datos.gov.co/index.php/usos/punto-seguro) (MinTIC), en el marco del concurso *Datos a la U 2024*.

## 📖 Descripción

Esta API centraliza el consumo y procesamiento de datos abiertos climáticos del IDEAM (precipitación, temperatura, presión atmosférica, humedad, viento) por estación meteorológica, y los combina con datos geoespaciales (Google Maps Geocoding) y modelos de predicción propios para ofrecer pronósticos climáticos por municipio a corto plazo. Sirve como backend para la app móvil [Punto Seguro](https://github.com/SergioRC-04/Punto-seguro).

## 🧠 Predicción climática

Uno de los componentes más interesantes del proyecto: los modelos de predicción **no se entrenan en la API**, sino en notebooks separados (`Modelos_Predi.ipynb`, `Predicciones Precipitaciones.ipynb`) usando `pandas` + `scikit-learn` (regresión lineal) sobre series históricas de las estaciones del IDEAM. Los modelos entrenados se serializan con `joblib`/`pickle` y se almacenan directamente como `BinaryField` en PostgreSQL (`ModelosPrediccion`, `ModelosPrediccionPrecipitacion`), listos para ser cargados y usados por la API bajo demanda vía el endpoint `/api/prediccion`.

## 🔌 Endpoints

Todos expuestos mediante `DefaultRouter` de DRF (CRUD completo por defecto en cada uno):

| Endpoint                     | Descripción                                                        |
| ------------------------------ | --------------------------------------------------------------------- |
| `/api/users`                  | Usuarios registrados.                                                |
| `/api/userlocation`           | Ubicación de casa y ubicación actual por usuario.                    |
| `/api/stations`               | Estaciones meteorológicas del IDEAM (nombre, municipio, coordenadas).|
| `/api/sensors`                | Sensores disponibles por estación (precipitación, temperatura, etc.).|
| `/api/observations`           | Lecturas históricas de los sensores.                                 |
| `/api/meetingpoint`           | Puntos de encuentro seguros ante una emergencia.                     |
| `/api/modelosprediccion`      | Modelos de predicción entrenados, serializados en la base de datos.  |
| `/api/prediccion`             | Predicciones climáticas generadas por municipio (hoy / mañana / pasado mañana). |

## 🛠️ Stack Técnico

| Componente            | Tecnología                        | Propósito                                                     |
| ----------------------- | ----------------------------------- | ----------------------------------------------------------------- |
| **Framework**          | Django 5.1 + Django REST Framework  | API REST y ORM.                                                  |
| **Base de datos**      | PostgreSQL (Aiven Cloud)            | Persistencia de usuarios, observaciones climáticas y modelos ML. |
| **Machine Learning**   | scikit-learn, pandas, joblib        | Entrenamiento y serialización de modelos de predicción por municipio. |
| **Geocodificación**    | Google Maps Platform                | Conversión de dirección de usuario a coordenadas.                |
| **Configuración**      | django-environ                      | Variables de entorno para credenciales.                          |
| **Servidor**           | Gunicorn + WhiteNoise                | Despliegue en producción (Koyeb) y archivos estáticos.           |

## 🏗️ Arquitectura

Este repositorio es la **API**. El cliente que la consume es la app móvil/web:

- **Cliente:** [`Punto-seguro`](https://github.com/SergioRC-04/Punto-seguro)

## 🚀 Cómo ejecutarlo localmente

```bash
git clone https://github.com/SergioRC-04/Punto_seguro_api.git
cd Punto_seguro_api
pip install -r requirements.txt
```

Crea un archivo `.env` en la raíz con:

```
DB_USER=tu_usuario
DB_PASSWORD=tu_password
GOOGLE_MAPS_API_KEY=tu_api_key
```

```bash
python manage.py runserver
```

La API estará disponible en `http://127.0.0.1:8000`.

## 👥 Equipo

Proyecto desarrollado en equipo para la convocatoria **"Datos a la U"** — Universidad del Norte, Ingeniería de Sistemas:

- Sergio Rodríguez
- Mariana Guerrero
- Sharik Bonadiez

## 📊 Fuentes de datos abiertos

- Registro Especial de Prestadores y Sedes de Servicios de Salud (REPS) — Datos.gov.co
- Precipitación, Presión Atmosférica, Dirección del Viento, Humedad del Aire a 2m — Datos.gov.co
- Datos Hidrometeorológicos Crudos, Red de Estaciones IDEAM: Temperatura — Datos.gov.co
- Recomendaciones — Defensa Civil Colombiana
