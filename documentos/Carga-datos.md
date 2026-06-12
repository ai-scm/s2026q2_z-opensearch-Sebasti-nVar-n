# Carga de datos

En esta etapa realizamos tanto la carga del dataset de ejemplo como la inyección de datos manuales para validar el comportamiento en tiempo real del dashboard.

## 1. Carga del Dataset Oficial
Para contar con una base de datos robusta, utilizamos los datos de muestra integrados en OpenSearch Dashboards:
* Accedimos al panel mediante `http://localhost:5601`.
* Seleccionamos la opción **"Add sample data"**.
* Cargamos específicamente el dataset: **Sample eCommerce orders**.
* Este dataset crea el índice `opensearch_dashboards_sample_data_ecommerce`, base de nuestro dashboard.

## 2. Verificación de Datos
Para confirmar que el índice fue creado correctamente, ejecutamos la siguiente consulta desde la terminal:
```bash
curl http://localhost:9200/opensearch_dashboards_sample_data_ecommerce/_count

3. Ingesta Manual (Prueba de Tiempo Real)
Para comprobar que el dashboard reac
ciona a los cambios en el índice, insertamos documentos manualmente mediante Dev Tools.

Ejemplo cargado:


POST opensearch_dashboards_sample_data_ecommerce/_doc/
{
  "customer_first_name": "Estudiante_Prueba",
  "category": ["Clothing"],
  "customer_gender": "MALE",
  "taxful_total_price": 2500.0,
  "order_date": "2026-06-12T11:30:00Z"
}

Tras ejecutar este comando y refrescar el dashboard, el monto de Total Ventas eCommerce se actualizó automáticamente, confirmando la persistencia y conectividad de los datos.

4. Configuración del Index Pattern
Para visualizar los datos, definimos el patrón en Stack Management → Index Patterns:

Nombre: opensearch_dashboards_sample_data_ecommerce

Campo de tiempo: order_date
