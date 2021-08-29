# kubernetsongcloud

Arquivos de deploy convertidos de um docker-compose

#aplicar o deploy convertido e expor a aplicação e o site com api

kubectl apply -f api-service.yaml,api-deployment.yaml,career-deployment.yaml,career-service.yaml,market-service.yaml,market-deployment.yaml,webapp-service.yaml,webapp-deployment.yaml,prodnet-networkpolicy.yaml 
kubectl expose deployment webapp --name webapplb --type LoadBalancer --port 3000 --target-port 3000
kubectl expose deployment api --name apilb --type LoadBalancer --port 8085 --target-port 8085


#verificaçao
kubectl get pods
kubectl logs -f career-7775f6d5cd-9247w
kubectl get service
kubectl describe deployment
