ACESSO EC2
    
    Link para acesso da maquina em nuvem com os containers rodando
    http://ec2-54-198-205-226.compute-1.amazonaws.com:8080/

NOTA
    
    Com a utilização do arquivo docker-compose não será mais necessário a utilização do diretorio phpapp que fica no repositório, o mesmo será mantido apenas para conferência de utilização sem a utilização do arquivo docker-compose


Criação dos containers locais 

Passo 1: Baixar os arquivos do repositorio mantendo as estruturas das pastas github.com/guigapc/scidevops

NGINX
    ####Para o nginx será utilizada a imagem guigapc/olamundo:v1 pois ja foi buildada e enviada ao docker hub com o arquivo default.conf correto para funcionamento do php-fpm, o arquivo default.conf utilizado na imagem esta na pasta nginx do repositório
    
    Este passo não precisa ser executado, apenas para ilustração de como foi feito
    Comando utilizado para build da imagem que ja foi enviada ao docker hub

    #docker build -t guigapc/olamundo:v1 .

PHP-FPM

    Passo 2: Entrar na pasta phpapp e executar a build da imagem utilizando o arquivo Dockerfile dentro da pasta

    docker build -t phpapp .

    Comando para criação dos containers passando a rede a ser utilizada, no caso foi criada uma network chama app-net
    Criar a network antes de executar a criação dos containers
    Comando para criação da rede dos containers

Criação da rede para os containers    
    
    docker network create app-net

Comando de criação dos containers

    docker run -d --name phpapp --network app-net -v $(pwd)/../www:/var/www/html phpapp && docker run -d --name ola-mundo --network app-net -p "8080:80" -v $(pwd)/../www:/var/www/html guigapc/olamundo:v1
