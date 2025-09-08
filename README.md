# Containerization

A home for my container learning, quick revisions, and production-style app containers.

- **`docker/`** → quick revision playground: tiny examples, beginner images, notes.
- **`apps/` (planned)** → real applications, each with its own Dockerfile and docs.
- **`compose/` (planned)** → Docker Compose stacks for local multi-service setups.
- **`k8s/` (planned)** → Kubernetes manifests / Helm charts.

> Keep experiments in `docker/`, and put real services in `apps/`. This separation keeps the repo tidy and avoids mixing throwaway examples with production-like code.

---

## Repository Structure

<pre>
Containerization/
├─ README.md
├─ docker/
│ └─ section-1/
│ └─ first-image/
│ ├─ Dockerfile
│ └─ app.py
├─ apps/ # planned
├─ compose/ # planned
└─ k8s/ # planned
</pre>

---

## Quick Start (current example)

Build and run the example located at `docker/section-1/first-image/`.

### 1) Build
```bash
docker build -t first-image:dev docker/section-1/first-image

# example I am using below command with docker user and repo details:-

docker build -t anshulawasthi03/first-image .

# or if you want to supply the path for your docker file

docker build -t anshulawasthi03/first-image docker/section-1/first-image
```
### 2) Run

Map the container port to your host (adjust ports to match the app inside the image—common choices are 5000 or 8000):

```bash
docker run --rm -it -p 8000:8000 first-image:dev
```
If your app.py serves on port 5000, use -p 5000:5000 instead.

### 3) Stop & Clean Up

Press Ctrl+C to stop an interactive container.

Optional cleanup:
```bash
docker ps -a
docker rm <container_id>        # remove stopped container
docker rmi first-image:dev      # remove image
```

### 4) Local Testing (without Docker)
```bash
cd docker/section-1/first-image
python app.py
```

If your app needs dependencies, add a requirements.txt here and install with:
```bash
pip install -r requirements.txt
```

### 5) Ignore Files

Keep a root .gitignore for global dev artefacts (e.g., __pycache__/, *.log, venv/, node_modules/, .env).

Keep a per-context .dockerignore next to each Dockerfile to keep images small:


## Helpful Docker Commands (Cheatsheet)

**Build with a tag**
```bash
docker build -t myimage:tag path/to/context
```

**Run interactively with port mapping**
```bash
docker run --rm -it -p HOSTPORT:CONTAINERPORT myimage:tag
```

**List images & containers**
```bash
docker images
docker ps -a
```

**Show logs**
```bash
docker logs -f <container_id_or_name>
```

**Remove containers & images**
```bash
docker rm <container_id>
docker rmi <image_id_or_tag>
```