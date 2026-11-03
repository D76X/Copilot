# Podman

[Podman Tutorial Zero to Hero | Full 1 Hour Course Amadeus for Developers](https://www.youtube.com/watch?v=YXfA5O5Mr18)  

[Podman vs. Docker IBM Technology](https://www.youtube.com/watch?v=Xx588nbshlM)  

[5 Podman Features You Should Know: Kubernetes & Containers Simplified IBM Technology and IBM Developer](https://www.youtube.com/watch?v=dEy3pQKhE8k)  

---

# Commands

| Command                                                                         | Meaning           | Notes |
| :------------------------------------------------------------------------------ | :---------------: | ----: |
| `podman images --format "table {{.Repository}}\t{{.Tag}}\t{{.Size}}\t{{.ID}}"`  |   pretty-format   | NA |
| `podman images --format "{{.Repository}}:{{.Tag}}"`                             |   pretty-format no headers | NA |
| `podman images --format "Image: {{.Repository}}:{{.Tag}} | Size: {{.Size}} | ID: {{.ID}}"`|   vertical layout   | NA |
| `podman images --format json | jq '.'`|   json output   | NA |
| `podman images --format json | jq '.'`|   json output   | NA |
| `podman ps -a --format "ID: {{.ID}}\nImage: {{.Image}}\nStatus: {{.Status}}\nName: {{.Names}}\n--------------"`|   vertical layout all containers   | NA |
| `podman ps -a --format "ID: {{.ID}}\nImage: {{.Image}}\nStatus: {{.Status}}\nName: {{.Names}}"`|   all containers no vertical layout  | NA |


---

> Tip: Create a Shell Alias

If you find a formatting command you like, you can save it as a permanent shortcut 
by adding an alias to your shell configuration file (such as `~/.bashrc`):

```
echo 'alias pimages="podman images --format \"table {{.Repository}}\t{{.Tag}}\t{{.Size}}\t{{.ID}}\""' >> ~/.bashrc
source ~/.bashrc
```

---


