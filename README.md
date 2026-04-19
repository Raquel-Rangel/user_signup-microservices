# User Registration Microservices | Spring Boot + RabbitMQ

### 🎯 Objetivo do Projeto
Sistema backend em arquitetura de microserviços que realiza cadastro de usuários com notificação assíncrona por e-mail. Desenvolvido para aplicar conceitos de **Event-Driven Architecture**, garantindo desacoplamento, escalabilidade e resiliência entre serviços.

### 🏗️ Arquitetura e Fluxo de Dados
 --POST--> [ms-user :8081] --publish--> [RabbitMQ Cloud] --consume--> [ms-email :8082] --SMTP-->
                          | |
                          ↓ ↓
                                                            [E-mail enviado]

1. **`ms-user`** expõe API REST para criação de usuários, persiste os dados em PostgreSQL e publica um evento `user.created` na fila.
2. **`ms-email`** consome eventos da fila de forma assíncrona e dispara e-mails de boas-vindas via Spring Mail + Gmail SMTP.

### 💡 Diferencial Técnico
Utilizando **comunicação assíncrona via message broker**, o sistema garante que a experiência do usuário no cadastro não seja impactada por lentidão ou indisponibilidade do serviço de e-mail. Essa abordagem segue padrões de mercado para sistemas distribuídos de alta disponibilidade.

### 🛠️ Stack Principal
`Java 17` `Spring Boot 3` `Spring AMQP` `RabbitMQ` `PostgreSQL` `JPA/Hibernate` `Spring Mail` `Maven` `UUID` `REST API`

### 🔑 Competências Demonstradas
- **Arquitetura de Microserviços:** Separação de responsabilidades e comunicação entre serviços
- **Mensageria:** Integração com RabbitMQ Cloud, produção e consumo de eventos
- **Persistência de Dados:** Modelagem com JPA/Hibernate e PostgreSQL
- **Integração Externa:** Configuração de envio de e-mails com autenticação segura (App Password)
- **Debugging e Troubleshooting:** Resolução de erros de conexão `ECONNREFUSED` e autenticação SMTP `530`
- **Boas Práticas:** Uso de UUID como PK, variáveis de ambiente, logs estruturados

### 🚀 Como Executar Localmente
1. Clone o repositório e configure as variáveis do `application.properties` em ambos os serviços
2. Suba uma instância do PostgreSQL e tenha as credenciais do RabbitMQ Cloud
3. Execute `ms-user` na porta 8081 e `ms-email` na porta 8082
4. Teste com `POST http://localhost:8081/users`
