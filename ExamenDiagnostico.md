### 📌 Instrucciones
Lee detenidamente cada pregunta y selecciona la respuesta correcta. Este es un examen de diagnóstico sin valor para la calificación final. Su propósito es identificar el nivel técnico del grupo. Por favor, no intentes adivinar; si desconoces por completo la respuesta a una pregunta, marca la opción **E) No sé la respuesta**.

---

### 1. Funciones de Ventana (Window Functions) y Empates
Considera una tabla `ventas` con una columna `monto`. Los valores ordenados de mayor a menor son: `100, 90, 90, 80`. Si aplicamos la función `DENSE_RANK() OVER (ORDER BY monto DESC)`, ¿qué secuencia de rangos se generará para estos 4 registros?

* **A)** 1, 2, 3, 4
* **B)** 1, 2, 2, 4
* **C)** 1, 2, 2, 3
* **D)** 1, 1, 1, 2
* **E)** No sé la respuesta

### 2. Optimización y Predicados SARGables
¿Cuál de las siguientes cláusulas `WHERE` sobre una columna `fecha_registro` (tipo `TIMESTAMP`) con un índice B-Tree permite al optimizador realizar un *Index Seek* eficiente (es decir, mantiene la condición SARGable)?

* **A)** `WHERE YEAR(fecha_registro) = 2023`
* **B)** `WHERE DATE(fecha_registro) >= '2023-01-01'`
* **C)** `WHERE fecha_registro >= '2023-01-01' AND fecha_registro < '2024-01-01'`
* **D)** `WHERE CAST(fecha_registro AS VARCHAR) LIKE '2023%'`
* **E)** No sé la respuesta

### 3. Lógica Tri-Valuada y Subconsultas
Dada la siguiente consulta: `SELECT * FROM tabla_a WHERE id NOT IN (SELECT id_fk FROM tabla_b)`. ¿Qué sucederá obligatoriamente si la subconsulta devuelve al menos un valor `NULL` entre sus resultados?

* **A)** La consulta ignorará el valor NULL y evaluará el resto de IDs de forma normal.
* **B)** La consulta devolverá un error de sintaxis en tiempo de ejecución.
* **C)** La consulta devolverá un conjunto de resultados vacío (cero filas), independientemente de los datos en `tabla_a`.
* **D)** La consulta devolverá todas las filas de `tabla_a`.
* **E)** No sé la respuesta

### 4. Expresiones de Tabla Comunes (CTEs) Recursivas
En la definición de una CTE recursiva estándar, ¿qué rol fundamental cumple el operador `UNION ALL` (o `UNION`)?

* **A)** Eliminar los registros duplicados antes de la siguiente iteración recursiva.
* **B)** Vincular el miembro ancla (la consulta inicial) con el miembro recursivo (la consulta que se itera).
* **C)** Limitar la profundidad de recursión para evitar bucles infinitos en el motor.
* **D)** Ordenar automáticamente los resultados jerárquicos nivel por nivel.
* **E)** No sé la respuesta

### 5. Orden Lógico de Ejecución de Consultas
¿En qué orden lógico procesa un motor de base de datos relacional estándar las siguientes cláusulas de una consulta SQL?

* **A)** SELECT -> FROM -> WHERE -> GROUP BY -> HAVING -> ORDER BY
* **B)** FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY
* **C)** FROM -> GROUP BY -> WHERE -> HAVING -> SELECT -> ORDER BY
* **D)** SELECT -> HAVING -> FROM -> WHERE -> GROUP BY -> ORDER BY
* **E)** No sé la respuesta

### 6. Agrupación y Filtrado de Conjuntos
Tienes una consulta que calcula el promedio de ventas por vendedor. Quieres incluir *únicamente* a los vendedores cuyo monto máximo en una sola venta superó los $500, pero calcular el promedio considerando *todas* sus ventas. ¿Dónde debes aplicar la condición `MAX(monto) > 500`?

* **A)** En la cláusula `WHERE`, usando una subconsulta correlacionada.
* **B)** En la cláusula `HAVING`.
* **C)** En el bloque `ON` de un `JOIN` con la misma tabla.
* **D)** En la cláusula `WHERE` estándar, antes del `GROUP BY`.
* **E)** No sé la respuesta

### 7. Cláusula OVER() y Particiones
¿Qué diferencia algorítmica principal existe entre aplicar `SUM(monto) OVER(PARTITION BY region)` frente a `SUM(monto) OVER(PARTITION BY region ORDER BY fecha)`?

* **A)** Ninguna, el resultado numérico para cada fila será exactamente el mismo.
* **B)** La primera calcula el gran total de la partición para cada fila; la segunda calcula una suma acumulativa (running total) basada en el orden de la fecha.
* **C)** La segunda devolverá un error porque `ORDER BY` no se permite dentro de `OVER` al usar `SUM`.
* **D)** La primera omite los valores nulos, mientras que la segunda los interpola.
* **E)** No sé la respuesta

### 8. Joins Múltiples y Agregaciones (Fan-out / Explosión de Joins)
Al realizar un `LEFT JOIN` desde una tabla `clientes` hacia dos tablas transaccionales de relación 1 a muchos (`facturas` y `pagos`) en la misma consulta, y aplicar un `SUM()` sobre los montos de ambas, ¿cuál es el riesgo principal si un cliente tiene múltiples facturas y múltiples pagos?

* **A)** Las funciones `SUM()` ignorarán los valores de la tabla `pagos` porque el primer JOIN bloquea los datos.
* **B)** Se producirá un producto cartesiano parcial, multiplicando artificialmente los montos sumados de ambas tablas.
* **C)** El motor de base de datos lanzará un error de "Agregación ambigua".
* **D)** Los totales serán correctos, pero la consulta será ineficiente debido al uso de memoria RAM.
* **E)** No sé la respuesta

### 9. Funciones de Agregación y Valores Nulos
En una tabla `empleados` con 4 registros, la columna `bono` tiene los siguientes valores: `1000, 1000, NULL, NULL`. ¿Qué resultado arrojará la consulta `SELECT SUM(bono) / COUNT(*) FROM empleados` comparado con `SELECT AVG(bono) FROM empleados`?

* **A)** Ambas consultas devolverán 500.
* **B)** Ambas consultas devolverán 1000.
* **C)** La primera devolverá 500 y la segunda devolverá 1000.
* **D)** La primera devolverá un error de división por cero y la segunda 1000.
* **E)** No sé la respuesta

### 10. Evaluación de Subconsultas y Rendimiento
Al optimizar una consulta relacional, ¿cuál es la principal ventaja algorítmica de utilizar `EXISTS (SELECT 1 ...)` en lugar de `IN (SELECT id ...)` cuando se evalúa la existencia de registros en una tabla secundaria de gran volumen?

* **A)** `EXISTS` permite realizar una "evaluación de cortocircuito" (short-circuit), deteniendo la búsqueda en la subconsulta al encontrar la primera coincidencia.
* **B)** `EXISTS` cachea automáticamente los resultados en memoria RAM, mientras que `IN` siempre lee del disco duro.
* **C)** `EXISTS` permite el uso de comodines (`%`), haciéndolo más flexible en texto que `IN`.
* **D)** `IN` no soporta índices B-Tree en la tabla secundaria, mientras que `EXISTS` los obliga a usarse.
* **E)** No sé la respuesta

---
