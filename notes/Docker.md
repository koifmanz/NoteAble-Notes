---
tags: [Notebooks/DevOps]
title: Docker
created: '2020-09-11T07:40:03.052Z'
modified: '2020-09-11T07:42:21.687Z'
---

# Docker

### How do I get into a Docker container's shell?

The docker exec command is probably what you are looking for; this will let you run arbitrary commands inside an existing container.

```bash
docker exec -it <mycontainer> bash
```

Of course, whatever command you are running must exist in the container filesystem, and if the container is running.
