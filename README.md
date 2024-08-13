Criação dos containers locais 
Baixar os arquivos do repositorio mantendo as estruturas das pastas
A imagem do nginx usar guigapc/olamundo:v1 pois ja foi buildada e enviada ao docker hub com o arquivo default.conf correto para funcionamento do php-fpm

#docker build -t guigapc/olamundo:v1 .

Entrar na pasta phpapp e executar a build da imagem utilizando o arquivo Dockerfile dentro da pasta
docker build -t phpapp .

Comando para criação dos containers passando a rede a ser utilizada, no caso foi criada uma network chama app-net
Criar a network antes de executar a criação dos containers
Comando para criação da rede dos containers
docker network create app-net


docker run -d --name phpapp --network app-net -v $(pwd)/../www:/var/www/html phpapp && docker run -d --name ola-mundo --network app-net -p "8080:80" -v $(pwd)/../www:/var/www/html guigapc/olamundo:v1
