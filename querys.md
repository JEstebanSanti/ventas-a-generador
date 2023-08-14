- Cuantas veces se ha vendido cada producto

SELECT sum(cantidad) FROM ventas_detalles WHERE nombre = "nombre_tu_producto" 

SELECT nombre, sum(cantidad) FROM ventas_detalles GROUP BY nombre;


- PRODUCTO MAS vendido

    SELECT nombre, sum(cantidad) FROM ventas_detalles GROUP BY nombre ORDER BY sum(cantidad) DESC LIMIT 1;

- PRODUCTO menos vendido
    SELECT nombre, sum(cantidad) FROM ventas_detalles GROUP BY nombre ORDER BY sum(cantidad) asc LIMIT 1;

- Producto nunca vendido

    SELECT productos.nombre, venta_detalle.nombre FROM productos LEFT join ventas_detalle on id_venta.ventas_detalles = id.ventas using(nombre) WHERE venta_detalle.nombre is null

- VENTA TOTAL en dinero

    SELECT nombre, sum(cantidad*precio) FROM ventas_detalles;

- VENTA FECHA hora Y cuanto fue

    SELECT ventas.id AS "VENTA ID", fecha, hora, SUM(cantidad*precio) AS "TOTAL VENTAS"  FROM ventas_detalle INNER JOIN ventas ON ventas_detalle.id_venta = ventas.id

- TOTAL VENTAS POR AÑO

    SELECT  fecha, sum(cantidad*precio) AS "TOTAL" FROM ventas INNER JOIN ventas_detalle ON ventas_detalle.id_venta = ventas.id group BY YEAR(fecha) order BY fecha ASC

- AÑO CON MENOR NUMERO DE VENTAS

    SELECT  fecha, sum(cantidad*precio) AS "TOTAL" FROM ventas INNER JOIN ventas_detalle ON ventas_detalle.id_venta = ventas.id group BY YEAR(fecha) order BY TOTAL ASC LIMIT 1

- AÑO CON MAYOR NUMERO DE VENTAS

    SELECT  fecha, sum(cantidad*precio) AS "TOTAL" FROM ventas INNER JOIN ventas_detalle ON ventas_detalle.id_venta = ventas.id group BY YEAR(fecha) order BY TOTAL DESC LIMIT 1

- VENTAS POR AÑO dinero y total de ventas 

    SELECT  YEAR(fecha), sum(cantidad*precio) AS "TOTAL", COUNT(*) AS "TOTAL DE VENTAS" FROM ventas INNER JOIN ventas_detalle ON ventas_detalle.id_venta = ventas.id group BY YEAR(fecha) order BY fecha ASC

- ARTICULO PRODUCTO MAS VENDIDO POR AÑO

    (SELECT  YEAR(fecha) AS "AÑO", sum(cantidad*precio) AS "TOTAL", nombre AS "NOMBRE", sum(cantidad) AS "CANTIDAD" FROM ventas INNER JOIN ventas_detalle ON ventas_detalle.id_venta = ventas.id group BY YEAR(fecha) order BY fecha ASC );


    SELECT 
    YEAR(v.fecha) AS "Año",
    SUM(vd.cantidad * vd.precio) AS "Total Ventas",
    vd.nombre AS "Nombre Producto",
    SUM(vd.cantidad) AS "Total Cantidad Vendida"
    FROM ventas v
    INNER JOIN ventas_detalle vd ON v.id = vd.id_venta
    GROUP BY YEAR(v.fecha), vd.nombre
    ORDER BY YEAR(v.fecha) ASC, "Total Ventas" DESC;





