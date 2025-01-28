# deepseek
local instance of deepseek

# Installing Ollama
docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama

# Pull the DeepSeek-R1 model
docker exec -it ollama ollama run deepseek-r1:7b

# Start chatting with DeepSeek-R1 - Web UI
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main

# Accessing the GUI on bowser 

http://localhost:3000

Create a test user: testuser/testuser

