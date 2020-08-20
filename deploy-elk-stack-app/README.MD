Deploy ELK Stack
docker-compose-elk.yaml is to deploy  ELK Stack 
docker-compose-app.yaml is to deploy KANBAN BOARDS app consist on three parts posrgre as database and kanban-app as background app to communicate with frontend and databbase kanban-ui code running in nginx logstash runs in this container and watch nginx's access and error logs and put them to elasticsearch in kibana dashboard need to create index kanban_ui* logs will be there in dashboard.
