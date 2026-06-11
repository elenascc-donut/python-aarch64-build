# Integrazione Python ARM64 con Yocto

## 📦 Contenuto dell'archivio

L'archivio `python-arm64.tar.gz` contiene:
- **Python 3.10.x** completo
- **pip** - gestore pacchetti Python
- **venv** - modulo per virtual environments
- **numpy** - computazione numerica
- **opencv-python** - computer vision
- **mss** - acquisizione schermo
- **pynput** - controllo mouse/tastiera

Tutto compilato per architettura **linux/arm64 (aarch64)**.

---

## 🚀 Uso in Yocto

### Step 1: Download archivio

Scarica l'archivio dalle **Releases** o dagli **Artifacts** del workflow GitHub Actions.

### Step 2: Estrai nell'ambiente di build

```bash
# Nel tuo build host (non nel target)
tar -xzf python-arm64.tar.gz -C /opt/

# Verifica
/opt/python-arm64/bin/python3 --version
/opt/python-arm64/bin/pip list