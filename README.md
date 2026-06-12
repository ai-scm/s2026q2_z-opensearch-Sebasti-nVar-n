# 📊 Dashboard de Analítica eCommerce - OpenSearch

Bienvenido al repositorio oficial del proyecto de **Analítica eCommerce**. Este proyecto documenta el despliegue, configuración y análisis de datos utilizando **OpenSearch Dashboards**.

---

## 🚀 Descripción del Proyecto
Este dashboard permite el monitoreo en tiempo real de ventas, tendencias temporales y segmentación por clientes, ofreciendo herramientas de **búsqueda faceteada** para un análisis de datos profundo y eficiente.

---

## 📂 Estructura del Repositorio
El proyecto está organizado para facilitar la revisión de cada etapa:

*   `01-instalacion/`: Guía de despliegue del entorno con Docker.
*   `02-Carga de datos/`: Scripts y ejemplos de carga manual de documentos JSON.
*   `03-dashboard/`: Configuración y lógica de las visualizaciones creadas.
*   `04-API rest/`: Documentación de las peticiones REST utilizadas.
*   `05-faceted search/`: Configuración detallada de los filtros interactivos.
*   `screenshots/`: Evidencia visual del funcionamiento del dashboard.

---

## 📈 Características Principales

| Componente | Descripción |
| :--- | :--- |
| **Métricas** | Visualización en tiempo real del `Sum` de ventas totales. |
| **Tendencias** | Gráfico de líneas detallado por `order_date`. |
| **Segmentación** | Gráficos de barras interactivos por Cliente y Categoría. |
| **Filtros** | Sistema de búsqueda faceteada para Ubicación, Fecha y Categoría. |

---

## 🛠️ Prueba de Tiempo Real
Para verificar que el dashboard reacciona ante nuevos datos, puedes ejecutar la siguiente consulta en **Dev Tools**:

```json
POST opensearch_dashboards_sample_data_ecommerce/_doc/
{
  "customer_first_name": "Cliente_VIP",
  "category": ["Clothing"],
  "customer_gender": "MALE",
  "taxful_total_price": 2500.0,
  "order_date": "2026-06-12T11:30:00Z"
}
