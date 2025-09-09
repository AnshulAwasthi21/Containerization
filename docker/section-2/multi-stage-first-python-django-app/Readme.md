## 🐳 Multi-Stage Dockerfile with venv

The idea:

* Stage 1 = Build image with compilers/tools, create venv, install dependencies.

* Stage 2 = Slim runtime image, copy only the venv + app code.

✅ Benefits:

* The final image is slim — it has only Python + venv + your code.

* Build dependencies (like gcc) don’t bloat the runtime image.

* All packages stay inside /opt/venv.