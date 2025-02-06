# Deepseek local instance running on Docker/Ollama

# Installing Ollama
docker run -d -v ollama:/root/.ollama -p 0.0.0.0:11434:11434 --name ollama ollama/ollama
docker run -d -v /home/hemas/llms:/models -p 0.0.0.0:11434:11434 --name ollama ollama/ollama

# Pull the DeepSeek-R1 model
docker exec -it ollama ollama run deepseek-r1:7b
docker exec -it ollama ollama run qwen2.5-coder:3b
docker exec -it ollama ollama run qwen2.5-coder:7b
docker exec -it ollama ollama run qwen2.5-coder:14b

# Start chatting with DeepSeek-R1 - Web UI
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main

# Accessing the GUI on bowser 
http://localhost:3000 - and Create a test user: testuser/testuser


# Deepseek local instance running on MicroK8s

- kubectl apply -f pv.yaml
- kubectl apply -f pvc.yaml
- kubectl apply -f deployment.yaml
- kubectl apply -f service.yaml

# Run the model as the resources you have - full model 671B
- kubectl exec $(kubectl get pods -n deepseek --no-headers -o custom-columns=":metadata.name") -n deepseek -- ollama run deepseek-r1:7b
- kubectl exec $(kubectl get pods -n deepseek --no-headers -o custom-columns=":metadata.name") -n deepseek -- ollama run deepseek-r1:70b-llama-distill-fp16

- kubectl apply -f pv-webgui.yaml
- kubectl apply -f pvc-webgui.yaml
- kubectl apply -f deployment-webgui.yaml
- kubectl apply -f service-webgui.yaml
- kubectl port-forward -n deepseek svc/open-webui-service 31434:8080

http://localhost:31434 - and Create a test user: testuser/testuser



- kubectl exec $(kubectl get pods -n ollama-qwer --no-headers -o custom-columns=":metadata.name") -n ollama-qwer -- ollama run qwen2.5-coder:7b