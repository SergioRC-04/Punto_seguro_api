# 🆘 Punto Seguro

> Plataforma móvil de preparación y respuesta comunitaria ante emergencias climáticas en Colombia.

[![Flutter](https://img.shields.io/badge/Flutter-3.x-02569B?style=flat-square&logo=flutter)]()
[![Plataformas](https://img.shields.io/badge/Plataformas-Android%20%7C%20iOS%20%7C%20Web-informational?style=flat-square)]()
[![Reconocimiento](https://img.shields.io/badge/Datos%20Abiertos%20Colombia-Proyecto%20Reconocido-green?style=flat-square)]()

🏆 **Este proyecto está registrado oficialmente en el portal de [Datos Abiertos de Colombia](https://herramientas.datos.gov.co/index.php/usos/punto-seguro) (MinTIC), en el marco del concurso *Datos a la U 2024*,** como caso de uso destacado de datos públicos con impacto social y ambiental.

---

## 📖 El problema

Colombia tiene comunidades rurales y urbanas altamente expuestas a inundaciones, deslizamientos y otras emergencias climáticas, con acceso limitado a información oportuna para actuar. **Punto Seguro** no es una app del clima: es una plataforma que cruza datos climáticos, geográficos y de seguridad pública en tiempo real, para que una persona sepa **qué está pasando cerca de ella y qué hacer al respecto**.

## 📱 Funcionalidades

- 🌦️ **Riesgo climático en tiempo real** según la ubicación del usuario, a partir de estaciones meteorológicas del IDEAM (precipitación, presión atmosférica, humedad, dirección del viento, temperatura).
- 📍 **Localización de puntos de emergencia** cercanos (centros de salud, puntos de encuentro seguros), usando el Registro Especial de Prestadores de Salud (REPS).
- 🗺️ **Rutas de evacuación** hacia zonas seguras.
- 💡 **Consejos de preparación y respuesta** ante emergencias, basados en recomendaciones de la Defensa Civil Colombiana.
- 👤 **Autenticación de usuarios** y perfil editable.
- 🔔 Diseñado para notificar a comunidades vulnerables sobre riesgos cercanos antes de que escalen.

## 🎬 Demo

Prototipo interactivo: **[app.flutterflow.io/share/punto-seguro-vs7akq](https://app.flutterflow.io/share/punto-seguro-vs7akq)**

> Si tienes capturas de pantalla o un GIF de la app corriendo, agrégalas aquí — es lo primero que mira un reclutador antes de leer texto.

## 🛠️ Stack Técnico

| Componente          | Tecnología                              | Propósito                                                        |
| -------------------- | ---------------------------------------- | ------------------------------------------------------------------ |
| **Framework**        | Flutter 3.x / Dart                       | App multiplataforma (Android, iOS, Web) desde un solo código base. |
| **UI Builder**       | FlutterFlow                              | Prototipado y construcción visual de las pantallas.                |
| **Enrutamiento**     | `go_router`                              | Navegación declarativa entre pantallas.                            |
| **Estado**           | `provider`                               | Manejo de estado de la aplicación.                                 |
| **Persistencia local**| `shared_preferences`, `sqflite`         | Datos de sesión y caché local.                                     |
| **Backend**          | API REST propia (desplegada en Koyeb)    | Autenticación, rutas, y datos de estaciones climáticas.            |
| **Mapas**            | Google Maps Platform                     | Visualización geoespacial de riesgos y rutas.                      |
| **Datos abiertos**   | Datos.gov.co (IDEAM, REPS)               | Fuente de los datos climáticos y de salud pública.                 |

## 🏗️ Arquitectura

Este repositorio contiene el **cliente móvil/web**. Se conecta a una API propia desplegada de forma independiente, responsable de la autenticación, la lógica de rutas y el consumo/normalización de los datasets del IDEAM:

- **API:** [`Punto_seguro_api`](https://github.com/sergio110304/Punto_seguro_api)

> 📝 Nota: el repositorio de la API está en una cuenta de GitHub distinta a la de este perfil. Si sigues usando ambos proyectos como parte de tu portafolio, vale la pena dejarlo claro en ambos README (o transferir/enlazar la cuenta) para que un reclutador no se confunda pensando que son de otra persona.

## 🚀 Cómo ejecutarlo localmente

```bash
git clone https://github.com/SergioRC-04/Punto-seguro.git
cd Punto-seguro
flutter pub get
flutter run
```

Requiere el [Punto_seguro_api](https://github.com/sergio110304/Punto_seguro_api) corriendo (local o el desplegado en Koyeb) para las funcionalidades de rutas, estaciones climáticas y autenticación.

## 👥 Equipo

Proyecto desarrollado en equipo para la convocatoria **"Datos a la U"** — Universidad del Norte, Ingeniería de Sistemas:

- Sergio Rodríguez
- Mariana Guerrero
- Sharik Bonadiez

## 📊 Fuentes de datos abiertos utilizadas

- Registro Especial de Prestadores y Sedes de Servicios de Salud (REPS) — Datos.gov.co
- Precipitación — Datos.gov.co
- Presión Atmosférica — Datos.gov.co
- Dirección del Viento — Datos.gov.co
- Humedad del Aire a 2 metros — Datos.gov.co
- Datos Hidrometeorológicos Crudos, Red de Estaciones IDEAM: Temperatura — Datos.gov.co
- Recomendaciones — Defensa Civil Colombiana

## 📄 Licencia

MIT License.
