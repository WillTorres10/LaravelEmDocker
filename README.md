
# Laravel em Docker
Esse repositório fornece o Docker Composer que permite execultar a Framework Laravel e com o Mysql (MariaDB) como Banco de Dados e o Nginx.

## Características
- Versão do Laravel: 7.14.1;
- Versão MariaDB: 10.5 (O docker-compose pega a mais recente disponível);
- Versão Nginx: 1.19 O docker-compose pega a mais recente disponível);
- Versão PHP: 7.2-fpm-alpine.

## Requisitos
- Docker
- Docker-Compose

## Estrutura do Projeto
- nginx | Pasta referente ao Volume para o serviço Nginx;
- mysql | Pasta referente ao Volume para o serviço Mysql;
- src | Local do Projeto do Laravel.

## Como Executar
Passo-a-passo para executar o projeto
####1. Clonando o Repositório
Copie o código abaixo e cole no terminal para clonar o repositório.

`$ git clone https://github.com/WillTorres10/LaravelEmDocker.git`

#### 2. Criando a pasta mysql
Após clonar o repositório, entre no diretório do respositório e crie uma pasta chamada **mysql**.

`$ mkdir mysql`

#### 3. Executando docker-composer
Para execultar e deixar o container funcionando execulte o comando abaixo:

`$ docker-composer build && docker-composer up -d`

#### 4. Configurando .env do Laravel
Acesse a pasta do Laravel:

`$ cd src `

Em seguida copie e renomeie o arquivo .env-example:

`$ cp .env.example .env`

Nas configurações de conexão com o banco, substitua  o trecho:

<pre>
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=
</pre>

por:

<pre>
DB_CONNECTION=mysql
DB_HOST=dbLaravel
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=laravel
DB_PASSWORD=laravel123
</pre>

e salve o arquivo.

#### 5. Concedendo permissão a pasta *storage*
O laravel pode dar erro de permissão negada para escrita da pasta storage. Para solucionar esse problema. Na pasta raiz do projeto clonado execute o seguinte comando:

`$ sudo chmod 777 -R ./src/storage/*`

#### 6. Executando Migrations
Para executar as Migrations na pasta raiz do projeto clonado digite o seguinte comando:

`$ docker-compose exec php php artisan migrate`

![Resultado Comando](https://i.imgur.com/FmI8zx6.png "Resultado Comando")

#### 7. Acessando página
Para acessar a página do laravel basta digitar no navegador a seguinte url:

`http://localhost:8088/`

o resultado esperado é esse:

[![Resultado Esperado](https://i.imgur.com/k0kimHB.png "Resultado Esperado")](http://localhost:8088 "Resultado Esperado")

## Portas
Detalhes das protas usadas pelos containers.
#### Porta Ngnix
- Interna: 80
- Externa: 8088

#### Porta Mysql
- Interna: 3306
- Externa: 4306

#### Porta PHP
- Interna: 9000
- Externa: 9000
