# Como criar um ambiente de desenvolvimento laravel utilizando docker

Partindo do princípio que em sua máquina tem instalado:

* git
* docker
* docker-compose


1. rodar comando 
        `git clone https://github.com/laravel/laravel.git <nome da aplicação>`

2. criar um container temporário do composer para montar os diretórios necessários para o projeto
        `docker run --rm -v $(pwd):/app composer install`

3. mover o arquivo docker-composer.yml e Dockerfile para dentro da raiz do projeto

4. Criar um diretório chamado nginx na raiz do projeto e dentro desse diretório criar outro diretório com o nome de conf.d

5. copiar o arquivo app.conf para dentro do diretório Raiz_do_Projeto/nginx/conf.d

6. rodar o comando `docker-compose up -d` 

7. copiar o arquivo .env-exemple para .env com o comando 
        `cp .env-exemple .env`

8. editar o arquivo .env com as mesmas configurações de banco de dados do docker-compose.yml

9. Obs: Todo comando php artisan a ser executado deve ser executado seguido de `docker-compose exec <comando>`

10. gerar chave do arquivo .env com o comando
        `docker-compose exec app  php artisan key:generate`

11. limpar a cache do projeto
        `docker-compose exec app php artisan config:cache`

12. Acessar a aplicação no navegador digitando localhost:80


13. Para gerenciar o banco de dados, abra o navegador e acessar o phpmyadmin através da url localhost:8080

14. Rodar as migrations (subir o banco)
        `docker-composer exec app php artisan migrate` 

15. **(opcional)** Alterar configurações do PHP

    * Criar na raiz do projeto uma pasta chamada php e criar um arquivo chamado local.ini
    * alterar no arquivo docker-compose.yml e na  parte de app: incluir a linha
    * - ./php/local.ini:/usr/local/etc/php/conf.d/local.ini
    * Após isso rodar o comando `docker-compose up -d`