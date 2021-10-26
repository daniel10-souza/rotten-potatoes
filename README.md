# rotten-potatoes
Projeto do Botcamp Kubdev com Fabricio Veronez
Setar as enviroments:

MONGODB_DB: admin
MONGODB_HOST: mongodb
MONGODB_PORT: 27017
MONGODB_USERNAME: mongouser
ONGODB_PASSWORD: mongopwd
MONGODB_DB => Nome do database
--
MONGODB_HOST => Host do MongoDB
MONGODB_PORT => Posta de acesso ao MongoDB
MONGODB_USERNAME => Usuário do MongoDB
MONGODB_PASSWORD => Senha do MongoDB

Comando para subir a aplicação
docker-compose --env-file ./.env up -d
*No caso do .env é preciso criar um arquivo .env na raiz para poder usar o parâmetro

