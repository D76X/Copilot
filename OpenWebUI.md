# Open Webui

[Open WebUI Documentation](https://docs.openwebui.com/)  
[open-webui](https://github.com/open-webui) 

---

##  Videos

[Gemma 4 Just Got Way More Powerful with Open WebUI Teacher's Tech](https://www.youtube.com/watch?v=aQ1rblXB91U&t=20s)

---

## How do I update Open Webui?

To update Open WebUI, how you proceed depends on your initial installation method:

- If you used Docker:

1. Stop and remove the old container by running: `docker rm -f open-webui`
2. Download the latest image: `docker pull ghcr.io/open-webui/open-webui:main`
3. Recreate and start the container with your previously used flags and volume mounts to preserve your data.

Alternatively, you can automate future updates by using a service like `Watchtower`.

- If you used pip (Python):

1. Stop your running instance (if applicable) by pressing `Ctrl + C` in your terminal.
2. Upgrade the package by running: `pip install --upgrade open-webui` 
3. If this fails to apply the new version, you can alternatively use `pip uninstall open-webui` followed by `pip install open-webui` to preserve user data while refreshing the build.
4. Restart the server with `open-webui serve`.

---

## How do I install OpenWebUI?

The recommended way to install Open WebUI is via Docker, which provides a fast setup with persistent data. 
Ensure you have Docker installed and either Ollama (for local models) or a cloud API key ready.
Quick Install (Docker)Run the following command in your terminal to start the container:bash

```
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

## Alternative Methods 

- GPU Support: 

If you have an NVIDIA GPU, add `--gpus all` and use the `:cuda` tag in the Docker command.

- Python (pip): 

For a native install, use pip install open-webui and run with open-webui serve.

- Desktop App: 

Downloadable installers are available on the GitHub releases page.Post-InstallationAfter launching, 
create your account, then navigate to Settings > Admin Settings > Connections to link your Ollama instance or add API keys.

---