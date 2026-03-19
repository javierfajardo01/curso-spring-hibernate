# Resultados — Bloque C‌‌‌​‌​‌‌​﻿‍‍​﻿‍‌​﻿​﻿​﻿​﻿​﻿​​‌‍​‌​﻿​﻿​﻿‍​​﻿‌​​﻿‌‌​﻿‌‍​﻿‌‍​﻿​‍​﻿‌﻿​﻿‌‌‌‍‌‌‌‍​‍

## Opcion elegida
[Validacion]

## Que implementaron
El proyecto Cine Estrella es una solución digital diseñada para automatizar la gestión integral de un complejo cinematográfico. Su objetivo es centralizar la información de la cartelera, las salas, la programación de sesiones y la venta de entradas, garantizando la coherencia y seguridad de los datos.
Funcionalidades Clave:
1. Gestión de Películas y Salas: Permite dar de alta, modificar y eliminar títulos y espacios físicos del cine.
2. Programación Inteligente: Al crear sesiones, el sistema valida la disponibilidad de salas y películas.
3. Venta de Entradas: Controla la asignación de asientos y precios por sesión.
4. Integridad de Datos: Gracias al borrado en cascada, si se elimina una sala o película, el sistema cancela automáticamente todas las sesiones y entradas asociadas para evitar errores.
Las siguientes capturas de Swagger demuestran las pruebas exitosas de la API, confirmando que el sistema responde correctamente a las operaciones de registro, consulta, actualización y eliminación de datos.

## Evidencia
![Captura de pantalla (2).png](../../img/Captura%20de%20pantalla%20%282%29.png)

## Codigo relevante (ejemplo de controlador REST)

/**
* Controlador REST para gestionar las operaciones relacionadas con las Películas.
* Proporciona endpoints para crear, leer, actualizar y eliminar (CRUD) películas,
* así como búsquedas específicas por clasificación.
  */
  @RestController
  @RequestMapping("/api/peliculas")
  public class PeliculaController {

  private final PeliculaService peliculaService;

  // Inyección de dependencias del servicio de películas
  public PeliculaController(PeliculaService peliculaService) {
  this.peliculaService = peliculaService;
  }

  /**
    * Obtiene una lista de todas las películas registradas en el sistema.
    *
    * @return Lista de objetos Pelicula.
      */
      @GetMapping
      public List<Pelicula> listarTodas() {
      return peliculaService.listarTodas();
      }

  /**
    * Busca una película específica por su ID.
    *
    * @param id El identificador único de la película.
    * @return ResponseEntity con la película si se encuentra (200 OK), o 404 Not Found si no existe.
      */
      @GetMapping("/{id}")
      public ResponseEntity<Pelicula> buscarPorId(@PathVariable Long id) {
      return peliculaService.buscarPorId(id)
      .map(ResponseEntity::ok)
      .orElse(ResponseEntity.notFound().build());
      }

  /**
    * Crea y registra una nueva película en la base de datos.
    *
    * @param pelicula El objeto Pelicula con los datos a guardar. Se valida antes de procesar.
    * @return La película creada con su ID generado y estado 201 Created.
      */
      @PostMapping
      public ResponseEntity<Pelicula> crear(@Valid @RequestBody Pelicula pelicula) {
      return ResponseEntity.status(HttpStatus.CREATED).body(peliculaService.crear(pelicula));
      }

  /**
    * Actualiza los datos de una película existente.
    *
    * @param id El ID de la película a actualizar.
    * @param pelicula Los nuevos datos de la película.
    * @return La película actualizada (200 OK) o 404 Not Found si el ID no existe.
      */
      @PutMapping("/{id}")
      public ResponseEntity<Pelicula> actualizar(@PathVariable Long id, @Valid @RequestBody Pelicula pelicula) {
      try {
      return ResponseEntity.ok(peliculaService.actualizar(id, pelicula));
      } catch (RuntimeException e) {
      return ResponseEntity.notFound().build();
      }
      }

  /**
    * Elimina una película del sistema por su ID.
    *
    * @param id El identificador de la película a eliminar.
    * @return 204 No Content si se elimina correctamente.
      */
      @DeleteMapping("/{id}")
      public ResponseEntity<Void> eliminar(@PathVariable Long id) {
      peliculaService.eliminar(id);
      return ResponseEntity.noContent().build();
      }

  /**
    * Busca películas filtrando por su clasificación (género).
    *
    * @param clasificacion El género de la película (ej. ACCION, DRAMA).
    * @return Lista de películas que coinciden con la clasificación.
      */
      @GetMapping("/clasificacion/{clasificacion}")
      public List<Pelicula> buscarPorClasificacion(@PathVariable Clasificacion clasificacion) {
      return peliculaService.buscarPorClasificacion(clasificacion);
      }
    }

