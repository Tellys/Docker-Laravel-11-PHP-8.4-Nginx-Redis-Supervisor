# Laravel 11 PHP 8.4 Nginx Redis Supervisor

Passo a passo da Criação do Docker com Laravel 11 + PHP 8.4 + Nginx + Redis + Supervisor

Neste repositório demostraremos como configurar um aplicativo PHP por vias do Framework Laravel, rodando em um servidor NGINX, PHP 8.4, Redis e Supervisor

A ideia é demostrar uma configuração básica, mas que abrirá várias possibilidades de escala-la em configurações mais robustas.

Lembrando que <b>aqui não estamos utilizando o Laravel Sail</b>. Aqui temos uma aplicação mais leve, uma vez que o SAIL carregaria todas as configurações necessárias para o funcionamento do Laravel.

# Imagem Docker

A imagem docker será capaz de criar containers com as seguintes aplicações:

- <b>PHP</b>, com várias extensões e Libs do PHP já configuradas, onde podemos enumerar algumas como: php-redis, pgsql, mysql, entre outras.

- <b>Nginx</b>, rodando como proxy reverso/servidor. Aqui deixamos a configuração bem tranquila, por vias do arquivo .conf

- <b>Supervisor</b>, que supervisionará as aplicações, viabilizando a execução da aplicação PHP (Laravel). Além de abrir a possibilidade futura de executarmos de filas e jobs.

- <b>Composer</b>, que será necessário para baixar e instar as dependências.

# Vídeos Tutorial

[Passo a passo da Criação do Docker com Laravel 11 + PHP 8.4 + Nginx + Redis + Supervisor](https://www.youtube.com/@tellyscastro5971)

# Passo a Passo para a instalção do Container Docker
- Aqui partimos do princípio que você já esteja com o Docker configurado em sua máquina, o qual será necessário para rodar os comandos abaixo.

## Verifique se seu docker esta rodando.

```sh
sudo docker compose version
```

## Agora confirme se algum container esta rodando
- Caso tenha algum container já rodando em sua máquina, pode ser interessante derrubá-lo, para não haver conflito nas portas 80 e 443, que iremos utilizar aqui

```sh
sudo docker ps
```

## Caso tenha container rodando derrube-os

```sh
sudo docker stop $(sudo docker ps -a -q)
```

## Caso seja necessário remover seus containers recentemente executados

```sh
sudo docker rm $(sudo docker ps -a -q)
```

## Caso seja preciso re iniciar seu Docker

```sh
sudo service docker restart
```

## Clone o Laravel
- Certifique-se de clonar o Larvel para uma pasta 'app'. Se ficar na dúvida veja o vídeo deste projeto.

- A listagem de pastas do projeto deve ficar:

```
    app/
    docker/
    .gitignore
    docker-compose.yml
    readme.md
```

## Build image Docker:

```sh
sudo docker compose build
```

## Para não utilizar o cache do seu docker
- Pode acontecer de o seu docker utilizar imagens já existentes em seu cache. Se isso ocasionar em erro, utilize o comando abaixo:

```sh
sudo docker compose build --no-cache
```

## Subindo a aplicação:

```sh
sudo docker compose up
```

- Para rodar o ambiente sem precisar manter o terminar aberto, execute:

```sh
sudo docker compose up -d
```

## Derrubar a aplicação:

```sh
sudo docker compose down
```

## Acessar comandos dentro do Container:

```sh
sudo docker ps
sudo docker exec -it id_do_container web bash
```

# Solução de Erros

## Erros de permissão

- não execute nada estando como o usuário root, pois vai dar erros.

- Para dar permissão ao seu usuário, temos os seguintes comandos

```sh
cd /var/www && \
chown -R www-data:www-data * && \
chmod -R o+w app
```
