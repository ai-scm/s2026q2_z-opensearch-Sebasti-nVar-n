# Faceted Search (Búsqueda Faceteada)

La búsqueda faceteada nos permite segmentar el volumen total de ventas combinando múltiples criterios de forma dinámica, replicando el comportamiento de un E-commerce real.

## 1. Configuración desde los Controles del Dashboard
Implementamos el componente **[eCommerce] Controls**, el cual permite aplicar filtros que actúan como "facetas" sobre el conjunto de datos de ventas. Los criterios configurados son:

* **Ubicación**: Filtrado por `geoip.city_name.keyword` para analizar ventas por ciudad.
* **Categoría**: Segmentación por `category.keyword` para ver el rendimiento de productos (ej. Ropa, Accesorios).
* **Filtro de Clientes**: Selección individual basada en `customer_first_name.keyword`.

Estos filtros operan bajo lógica **AND**, permitiendo aislar transacciones específicas (por ejemplo: Ventas de categoría 'Clothing' realizadas en una ciudad específica).

## 2. Implementación técnica (Query DSL)
Esta capacidad de segmentación se basa en consultas de tipo `bool` con filtros `must` o `filter`. Ejemplo de una búsqueda para ventas de una categoría y género específicos:

```json
GET opensearch_dashboards_sample_data_ecommerce/_search
{
  "query": {
    "bool": {
      "must": [
        { "term": { "category.keyword": "Clothing" } },
        { "term": { "customer_gender.keyword": "MALE" } }
      ]
    }
  }
}
3. Agregaciones para Facetas
Para alimentar los controles del dashboard, utilizamos agregaciones de tipo terms, que nos permiten obtener los conteos rápidos para cada filtro:

GET opensearch_dashboards_sample_data_ecommerce/_search
{
  "size": 0,
  "aggs": {
    "ventas_por_categoria": {
      "terms": { "field": "category.keyword" }
    },
    "ventas_por_genero": {
      "terms": { "field": "customer_gender.keyword" }
    }
  }
}
Resultado: Obtenemos el conteo de pedidos agrupado automáticamente, lo que permite al usuario final seleccionar rápidamente las categorías o géneros disponibles sin escribir consultas complejas.
