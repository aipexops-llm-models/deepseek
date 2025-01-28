# Deepseek local instance running on Ollama

# Installing Ollama
docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama

# Pull the DeepSeek-R1 model
docker exec -it ollama ollama run deepseek-r1:7b

# Start chatting with DeepSeek-R1 - Web UI
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main

# Accessing the GUI on bowser 
http://localhost:3000 - and Create a test user: testuser/testuser


# On MicroK8s

kubectl apply -f pv.yaml
kubectl apply -f pvc.yaml
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl exec ollama-deployment-59b5448559-p9r7r -n deepseek -- ollama run deepseek-r1:7b

kubectl apply -f pv-webgui.yaml
kubectl apply -f pvc-webgui.yaml
kubectl apply -f deployment-webgui.yaml
kubectl apply -f service-webgui.yaml
kubectl port-forward -n deepseek svc/open-webui-service 31434:8080
