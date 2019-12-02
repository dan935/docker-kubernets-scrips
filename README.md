docker-kubernets-scrips

aqui estan los comandos en debian necesarios para instalar docker y docker compost

-Actualizamos nuestra lista de paquetes
sudo apt update

-Instalamos algunos pre requisitios para usar el appt use paquetes que vienen por https
sudo apt update

-Agregamos la llave GPG del repositorio oficial de docker
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -

-Agrega,ps eñ repositorio de docker a nuestras fuentes de apt
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"

-Volvemos a actualizar nuestros paquetes pero ahora con los paquetes de docker agregados
sudo apt update

-Finalmente instalamos docker
-sudo apt install docker-ce

-Instalando compose
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

-Le damos permisos de ejecucion al binario
sudo chmod +x /usr/local/bin/docker-compose

para instalar kublect

sudo apt-get update && sudo apt-get install -y apt-transport-https
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl

Instalar minikube

curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && chmod +x minikube

agregar minikube como comando ejecutable

sudo mkdir -p /usr/local/bin/
sudo install minikube /usr/local/bin/

Comandos para desplegar la aplicacion de django

docker-compose build

docker-compose up

y ya solo acceder al localhost en el puerto 8000

Comandos para desplegar la aplicacion de PHP

Construimos las imagenes de docker que van a ser usadas por los pods

docker build -t redis-local -f Dockerfile-redis .

docker build -t php-apache-gke -f Dockerfile-php .

Una vez establesidas las imahenes mapear el redishost para que nuestro pod de php se pueda conectar al pod de redis

kubectl create configmap redishost --from-literal=REDIS_HOST=redis --from-literal=REDIS_PORT=6379

lanzamos nuestros pods

kubectl apply -f redis.yaml

kubectl apply -f php-apache.yaml

Verificamos que los pods esten corriendo y los servicios con

 kubectl get pods  

 kubectl get services

Find your service url using

`minikube service php-apache --url`