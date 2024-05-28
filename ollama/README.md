Install `ollama` [^KKSCn]

[^KKSCn]: Ollama on Linux, GitHub  
<https://github.com/ollama/ollama/blob/main/docs/linux.md>

```bash
curl -L https://ollama.com/download/ollama-linux-amd64 -o /usr/bin/ollama
chmod +x /usr/bin/ollama
useradd -r -s /bin/false -m -d /usr/share/ollama ollama
cat > /etc/systemd/system/ollama.service <<EOF
[Unit]
Description=Ollama Service
After=network-online.target

[Service]
ExecStart=/usr/bin/ollama serve
User=ollama
Group=ollama
Restart=always
RestartSec=3

[Install]
WantedBy=default.target
EOF
systemctl daemon-reload ; systemctl enable --now ollama
```

Download a model [^mcEwD]:

[^mcEwD]: Ollama Models, Ollama Project  
<https://ollama.com/library>

```bash
ollama pull llama3
```

Install a web UI [^Paxbk]:

[^Paxbk]: Open WebUI for Ollama, Github  
<https://github.com/open-webui/open-webui>

```bash
podman run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway \
            -v open-webui:/app/backend/data --name open-webui \
            --restart always ghcr.io/open-webui/open-webui:main
```

