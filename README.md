# N8N

Para uso local do automatizador de fluxograma [N8N](https://n8n.io), bem como containers do [PGVector](https://github.com/pgvector/pgvector) e do [WAHA - WhatsApp API](https://waha.devlike.pro).

Baseado na [configuração de _deploy_ do N8N usando Docker](https://docs.n8n.io/hosting/installation/server-setups/docker-compose/).

## Deploy

> **Atenção!** No MacOS faça: `docker pull devlikeapro/waha:arm && docker tag devlikeapro/waha:arm devlikeapro/waha:latest`.

Preparação do ambiente:

```
docker network create my_n8n_network && \
docker volume create my_n8n_db && \
docker volume create my_n8n_data && \
docker volume create my_n8n_vector && \
docker volume create my_n8n_pgadmin && \
docker volume create my_n8n_waha && \
docker volume create --driver local --opt type=none --opt device=$(pwd)/backup --opt o=bind my_n8n_backup
```

Configuração das variáveis de ambiente:

```
cp .env.example .env
```

Subir a _stack_ de containers:

```
docker compose up --force-recreate --build --remove-orphans --wait
```

## Community Nodes

É necessário [instalar dois _community nodes_](https://docs.n8n.io/integrations/community-nodes/installation/gui-install/#install-a-community-node) para utilizar os _workflows_ como **MCP Servers** e com a **WAHA WhatsApp API**, respectivamente:

- `n8n-nodes-mcp`
- `@devlikeapro/n8n-nodes-waha`

## Referências

- https://www.youtube.com/watch?v=g3sXsi_OYqQ&t=1575s
- https://comunidadezdg.com.br/waha-n8n/
- https://waha.devlike.pro/docs/overview/quick-start/

## Anotações

Dica para subir os dados de um BD PGVector (onde os vetores são gerados) para outro (onde serão utilizados pelo N8N):

```
pg_dump -C -t vectors_phi4_14b -h localhost n8n_vector -U vector | psql -h cloud.agro.rocks -U vector -p 49212 n8n_vector
```
