---
title: GitPod
tags:
  - CI/CD
  - GitPod
---

# GitPod

## Prebuilding and Workspace Image

By default, Gitpod uses a standard Docker Image called `Workspace-Full` as the foundation for workspaces. Workspaces started based on this default image come pre-installed with Docker, Nix, Go, Java, Node.js, C/C++, Python, Ruby, Rust, Clojure as well as tools such as Homebrew, Tailscale, Nginx and several more.


### Using Public Docker Image

```yml title=".gitpod.yml"
image: node:buster
```

!!! note

    Gitpod supports Debian/Ubuntu based Docker images. Alpine images do not include libgcc and libstdc++ which breaks Visual Studio Code. 

### Using Custom Docker Image

```yml title=".gitpod.yml"
image:
  file: .gitpod.Dockerfile
```

```dockerfile title=".gitpod.Dockerfile"
# Public Image
FROM gitpod/workspace-full:latest

# Install custom tools, runtime, etc.
RUN brew install fzf
```
