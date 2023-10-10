
# Ambiente Docker Multi-Serviço

Este repositório contém um ambiente Docker configurado com vários serviços, incluindo PHP, MySQL, phpMyAdmin, MailHog, Node.js, MongoDB, Redis e Apache Airflow. Siga as instruções abaixo para usar e configurar cada serviço.

## Pré-requisitos

Antes de começar, certifique-se de ter o Docker e o Docker Compose instalados em sua máquina.

- Docker: [Instalação do Docker](https://docs.docker.com/get-docker/)
- Docker Compose: [Instalação do Docker Compose](https://docs.docker.com/compose/install/)

## Instruções de Uso

1. **Clonar o repositório:**

   Clone este repositório em sua máquina local:

   ```shell
   git clone git@github.com:lotustea/docker-config-vps.git
   cd docker-config-vps
   ```

2. **Persistência de Dados:**

   Crie as seguintes pastas no diretório raiz do projeto para persistência de dados dos serviços:

   - `php` para persistência de arquivos PHP.
   - `mysql` para persistência de dados do MySQL.
   - `mongo_data` para persistência de dados do MongoDB.
   - `node` para persistência de arquivos Node.js.
   - `nginx` para configuração do Nginx.

3. **Configuração do Nginx:**

   Dentro da pasta `nginx`, crie um arquivo de configuração chamado `default.conf`. Personalize este arquivo para configurar o roteamento das suas aplicações PHP e Node.js. Aqui está um exemplo básico de configuração:

   ```nginx
   server {
       listen 80;
       server_name localhost;

       location /php {
           proxy_pass http://php;
       }

       location /node {
           proxy_pass http://node;
       }

       # ... outras configurações ...
   }
   ```

4. **Iniciar os Serviços:**

   Execute o seguinte comando para iniciar todos os serviços em segundo plano:

   ```shell
   docker-compose up -d
   ```

5. **Acessar os Serviços:**

   - **Aplicativo PHP:** http://localhost
   - **phpMyAdmin:** http://localhost:8080
   - **Aplicativo Node.js:** http://localhost:3000
   - **MailHog (para testes de email):** http://localhost:8025
   - **Apache Airflow:** http://localhost:8081

## Detalhes dos Serviços

### PHP:

- **Imagem Docker:** php:7.4.12-apache
- **Porta:** 80
- **Pasta de Persistência:** ./php

### MySQL:

- **Imagem Docker:** mysql:latest
- **Porta:** 3306
- **Variáveis de Ambiente:**
  - MYSQL_ROOT_PASSWORD: Root123
  - MYSQL_DATABASE: lt_db_lsd
  - MYSQL_USER: lotusta
  - MYSQL_PASSWORD: lous123tea
- **Pasta de Persistência:** ./mysql

### phpMyAdmin:

- **Imagem Docker:** phpmyadmin/phpmyadmin
- **Porta:** 8080
- **Variáveis de Ambiente:**
  - PMA_HOST: mysql
  - PMA_USER: lotustea
  - PMA_PASSWORD: lotus123tea

### MailHog:

- **Imagem Docker:** mailhog/mailhog
- **Porta:** 8025

### Node.js:

- **Imagem Docker:** node:latest
- **Porta:** 3000
- **Pasta de Persistência:** ./node

### MongoDB:

- **Imagem Docker:** mongo:latest
- **Porta:** 27017
- **Pasta de Persistência:** ./mongo_data

### Redis:

- **Imagem Docker:** redis:latest
- **Porta:** 6379

### Apache Airflow:

- **Imagem Docker:** puckel/docker-airflow
- **Porta:** 8081
- **Variáveis de Ambiente:**
  - LOAD_EX=n
  - EXECUTOR=Local

## Encerrar os Serviços

Para encerrar todos os serviços e liberar os recursos, execute:

```shell
docker-compose down
```

## Contribuições

Contribuições são bem-vindas. Crie Issues ou envie Pull Requests para melhorias ou correções.

## Licença

Este projeto está sob a Licença MIT. Consulte o arquivo [LICENSE](LICENSE) para obter detalhes.
```

Certifique-se de personalizar este `README.md` com informações específicas do seu projeto, como links relevantes, nomes de imagens Docker personalizadas ou configurações adicionais de serviços, conforme necessário. Este README fornece detalhes completos sobre como usar e configurar cada serviço no ambiente Docker.
