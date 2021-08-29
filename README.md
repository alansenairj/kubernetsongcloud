# kubernetsongcloud
!!!readme em processo de construção. ainda falta integrar os comandos usados para configurar o cli do gcloud. 

# 1- Converter o docker-compose em kubernets resources

com o arquivo docker-compose pronto, parte-se do princípio que as imagens estão disponibilizadas em um registry público

# 1.1 - instalaçao do Kompose
curl -L https://github.com/kubernetes/kompose/releases/download/v1.22.0/kompose-linux-amd64 -o kompose
chmod +x kompose
sudo mv ./kompose /usr/local/bin/kompose

# 1.2 executar a conversão na mesma pasta que contém o docker-compose

kompose convert
ls

# 2 criar o cluster

gcloud container clusters create webapp --zone us-west1-a
gcloud container clusters get-credentials webapp \
     --zone us-west1-a


# 3 aplicar o deploy convertido e expor a aplicação e o site com api

kubectl apply -f api-service.yaml,api-deployment.yaml,career-deployment.yaml,career-service.yaml,market-service.yaml,market-deployment.yaml,webapp-service.yaml,webapp-deployment.yaml,prodnet-networkpolicy.yaml 
kubectl expose deployment webapp --name webapplb --type LoadBalancer --port 3000 --target-port 3000
kubectl expose deployment api --name apilb --type LoadBalancer --port 8085 --target-port 8085


# 4 verificaçao
kubectl get pods
kubectl logs -f career-7775f6d5cd-9247w
kubectl get service
kubectl describe deployment
