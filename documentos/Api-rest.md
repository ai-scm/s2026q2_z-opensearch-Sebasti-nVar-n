# Exploración de la API REST

OpenSearch expone una API REST en `http://localhost:9200`. Hemos utilizado esta API para gestionar y consultar nuestro índice de eCommerce de forma directa, tanto desde la terminal como desde **Dev Tools**.

## 1. Operaciones principales vía API
Utilizamos las siguientes consultas para auditar y gestionar nuestra base de datos de ventas:

*   **Explorar estructura (Mapping)**: Para conocer los tipos de datos de los campos de ventas (ej. `taxful_total_price` como float, `order_date` como date).
```json
    GET opensearch_dashboards_sample_data_ecommerce/_mapping
    ```

*   **Contar transacciones**: Verificación del volumen total de pedidos.
```json
    GET opensearch_dashboards_sample_data_ecommerce/_count
    ```

*   **Obtener un registro de muestra**: Para visualizar la estructura real de un pedido.
```json
    GET opensearch_dashboards_sample_data_ecommerce/_search
    { "size": 1 }
    ```

## 2. Consultas Analíticas (Agregaciones)
Para obtener métricas rápidas sin necesidad de procesar los documentos individualmente, utilizamos agregaciones. Por ejemplo, para ver el total de ventas por categoría:

```json
GET opensearch_dashboards_sample_data_ecommerce/_search
{
  "size": 0,
  "aggs": {
    "ventas_por_categoria": {
      "terms": { "field": "category.keyword" }
    }
  }
}

3. Comparativa de Herramientas
Para este proyecto, diferenciamos el uso de las herramientas según la necesidad:

Aspecto                   curl(Terminal)                         Dev Tools(UI)

Uso principal	            Pruebas de conectividad                Desarrollo interactivo y 
                          rápidas y scripts                      visualización JSON


Sintaxis                  Comandos de una sola línea             JSON formateado multi-línea


Entorno                   Línea de comandos (Ubuntu)             Navegador (Port 5601)


Nota: Todas las consultas fueron validadas contra nuestro índice de eCommerce, garantizando
que los campos category, customer_first_name y taxful_total_price respondieran
correctamente a las peticiones.




