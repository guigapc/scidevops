Criação dos containers locais 

docker build -t guigapc/olamundo:v1 .
docker build -t phpapp .

docker run -d --name phpapp --network app-net -v $(pwd)/../www:/var/www/html phpapp && docker run -d --name ola-mundo --network app-net -p "8080:80" -v $(pwd)/../www:/var/www/html guigapc/olamundo:v1
