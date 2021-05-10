
## Sobre CQRS - Segregação de responsabilidade de consulta de comando
De acordo com Martin Folwer

Em seu cerne está a noção de que você pode usar um modelo diferente para atualizar as informações do modelo que você usa para ler as informações. Para algumas situações, essa separação pode ser valiosa, mas tome cuidado, pois para a maioria dos sistemas, o CQRS adiciona uma complexidade arriscada.

##A aplicação
Simula um cenário de conta bancária em que um usuário final adiciona uma transação de receita ou despesa e é processado em uma fonte de eventos ascíncrona e arquitetura CQRS para recalcular o saldo da conta bancária do usuário. O usuário também pode solicitar o saldo de sua conta. Aqui embaixo você pode ver o design:



## Implantar os serviços externos
docker-compose up -d --build
####Ele implantará quatro contêineres docker em seu ambiente com MongoDB, PostgreSQL, Kafka e Zookepper (exigido por Kafka)

Depois de implantar o Kafka, você precisará criar o tópico no cluster Kafka.

## Testando o aplicativo
####Executar uma solicitação CURL para criar uma transação de receita
curl -X POST -H "Content-Type: application / json" -d @ income-transaction.json http: // localhost: 8080 / transactions

####Executar uma solicitação CURL para criar uma transação de despesas
curl -X POST -H "Content-Type: application / json" -d @ expens-transaction.json http: // localhost: 8080 / transactions

####Solicitação CURL em execução para buscar o equilíbrio
curl http: // localhost: 8081 / balance \? accountId \ = wesley | json_pp

####Executando o teste de desempenho simples do K6
k6 run --vus 10 --duration 60s performance-tests / income.js
k6 run --vus 10 --duration 60s performance-tests / expens.js

##Contribuindo
####Eu adoraria ter uma interface para ele! Por favor, me contate se você se interessar

