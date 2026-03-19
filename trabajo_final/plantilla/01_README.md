# Trabajo Final — Javier Fajardo Tábara‌‌‌​‌​‌‌​﻿‍‍‌‍​‍​﻿​﻿​﻿​‍​﻿‌‌‌‍‌​‌‍​‍‌‍‌‍‌‍​‌​﻿‌‌​﻿‍‌‌‍​‌‌‍​‌​﻿​‍‌‍‌​​﻿‍‌‌‍‌‌

## Blueprint elegido
Cine Estrella

## Descripcion
La API de Cine-Estrella proporciona una interfaz RESTful para gestionar la
información de un cine, incluyendo películas, salas, sesiones y la venta de
entradas.

## Entidades

| Entidad  | Campos principales                                       | Relaciones                                                         |
|----------|----------------------------------------------------------|--------------------------------------------------------------------|
| Pelicula | id, titulo, duracion, director, clasificacion, sesiones  | ManyToOne con Sesiones                                             |
| Sala     | id, numero, capacidadMaxima, tiene3D, sesiones           | ManyToOne con Sesiones                                             |
| Entrada  | id, asiento, nombreCliente, sesion                       | ManyToOne con Sesiones                                             |
| Sesion   | id, fechaHora, precio, pelicula, sala, entradas          | ManyToOne con Pelicula, ManyToOne con Sala, ManyToOne con Entrada  |

## Endpoints de la API

| Verbo  | URL                                                | Descripcion                  |
|--------|----------------------------------------------------|------------------------------|
| GET    | `/api/peliculas`                                   | Listar peliculas             |
| GET    | `/api/peliculas/{id}`                              | Buscar por Id                |
| GET    | `/api/peliculas/{clasificacion}`                   | Buscar por clasif.           |
| POST   | `/api/peliculas`                                   | Crear pelicula               |
| DELETE | `/api/peliculas/{id}`                              | Borrar por Id                |
| PUT    | `/api/peliculas/{id}`                              | Modificar por Id             |
| GET    | `/api/sesiones`                                    | Listar sesiones              |
| GET    | `/api/sesiones/{id}`                               | Buscar por Id                |
| POST   | `/api/sesiones`                                    | Crear sesion                 |
| DELETE | `/api/sesiones/{id}`                               | Borrar por Id                |
| PUT    | `/api/sesiones/{id}`                               | Modificar por Id             |
| GET    | `/api/sala`                                        | Listar salas                 |
| GET    | `/api/sala/{id}`                                   | Buscar por Id                |
| POST   | `/api/sala`                                        | Crear sala                   |
| DELETE | `/api/sala/{id}`                                   | Borrar por Id                |
| PUT    | `/api/sala/{id}`                                   | Modificar por Id             |
| GET    | `/api/entradas`                                    | Listar entradas              |
| GET    | `/api/entradas/{id}`                               | Buscar por Id                |
| POST   | `/api/entradas`                                    | Crear entradas               |
| DELETE | `/api/entradas/{id}`                               | Borrar por Id                |
| PUT    | `/api/entradas/{id}`                               | Modificar por Id             |
| GET    | `/api/entradas/sesion/{sesionId}`                  | Buscar por sesion            |
| GET    | `/api/entradas/sesion/{sesionId}/asiento{asiento}` | Buscar por sesion y asiento  |
| GET    | `/api/entradas/nombre/{nombreCliente}`             | Buscar por nombre de cliente |
| GET    | `/api/entradas/asiento/{asiento}`                  | Buscar por asiento           |

## Como ejecutar

```bash
# Con Docker
docker compose up --build -d

# Sin Docker (H2)
mvn spring-boot:run
```
