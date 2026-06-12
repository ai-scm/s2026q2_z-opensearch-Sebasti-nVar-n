# 03 — Dashboard y visualizaciones

Todas las visualizaciones fueron creadas desde la sección **Visualize** en OpenSearch Dashboards, utilizando el índice `opensearch_dashboards_sample_data_ecommerce` para monitorear el rendimiento de la tienda.

## Visualización 1 — Total Ventas eCommerce (Métrica)
Muestra el valor monetario acumulado de todas las transacciones dentro del periodo seleccionado.
* **Tipo**: Metric
* **Configuración**: 
    * **Aggregation**: Sum
    * **Field**: `taxful_total_price`
* **Utilidad**: Actúa como nuestro KPI principal para medir el rendimiento financiero del eCommerce.

## Visualización 2 — Ventas por Cliente (Gráfico de Barras)
Muestra la distribución de la actividad de los clientes, permitiendo identificar a los más frecuentes.
* **Tipo**: Bar
* **Configuración**:
    * **Metrics (Y-Axis)**: Count
    * **Buckets (X-Axis)**: Terms → Field: `customer_first_name.keyword`
* **Utilidad**: Permite identificar qué clientes generan mayor volumen de pedidos.

## Visualización 3 — Tendencia de Pedidos (Gráfico de Líneas)
Visualiza la evolución de la cantidad de pedidos realizados en el tiempo.
* **Tipo**: Line
* **Configuración**:
    * **Metrics (Y-Axis)**: Count
    * **Buckets (X-Axis)**: Date Histogram → Field: `order_date` → Interval: Auto
* **Utilidad**: Útil para detectar picos de demanda y planificar la disponibilidad del servicio.

---

## Creación del Dashboard
Integramos las visualizaciones anteriores en un tablero centralizado:
1. Navegamos a **Dashboard** → **Create dashboard**.
2. Añadimos las tres visualizaciones creadas.
3. Organizamos el layout arrastrando los paneles para optimizar la visualización de datos.
4. **Guardado**: El tablero se guardó bajo el nombre "Dashboard eCommerce Final".

---
*Resultado: Un tablero interactivo que permite visualizar el flujo de ingresos y el comportamiento de compra en tiempo real.*
