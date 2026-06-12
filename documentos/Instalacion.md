# 01 — Instalación de Docker y OpenSearch

Para el despliegue del entorno de análisis de datos, se configuró un cluster de un solo nodo de **OpenSearch** junto con **OpenSearch Dashboards** mediante contenedores Docker.

## 1. Configuración del Sistema
Se realizó el ajuste obligatorio de memoria para el kernel, permitiendo que OpenSearch gestione correctamente la memoria asignada:
```bash
sudo sysctl -w vm.max_map_count=262144
echo "vm.max_map_count=262144" | sudo tee -a /etc/sysctl.conf

2. Definición del entorno (docker-compose.yml)
Se utilizó la versión 3.6.0 con la seguridad deshabilitada (DISABLE_SECURITY_PLUGIN=true) para optimizar el desarrollo local.

services:
  opensearch:
    image: opensearchproject/opensearch:3.6.0
    container_name: opensearch
    environment:
      - cluster.name=opensearch-cluster
      - node.name=opensearch-node1
      - discovery.type=single-node
      - OPENSEARCH_JAVA_OPTS=-Xms1g -Xmx1g
      - DISABLE_SECURITY_PLUGI
N=true
    ports:
      - "9200:9200"
      - "5601:5601"
    # ... resto de la configuración

3. Despliegue y Verificación
Para iniciar los servicios:

docker compose up -d

Para verificar que el nodo responde correctamente:

curl http://localhost:9200

Respuesta esperada: "number" : "3.6.0"
