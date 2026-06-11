# Python ARM64 Builder for Yocto

Questo repository contiene uno script di **GitHub Actions** per compilare **Python 3.10** con dipendenze comuni per architettura **ARM64/aarch64** pronto per l'uso in Yocto.

## 🎯 Cosa si ottiene

Un archivio **tar.gz** contenente:
- ✅ **Python 3.10.x** completo
- ✅ **pip** - gestore pacchetti
- ✅ **venv** - ambienti virtuali
- ✅ **numpy** - computazione numerica
- ✅ **opencv-python** - computer vision
- ✅ **mss** - acquisizione schermo
- ✅ **pynput** - controllo periferiche

**Tutto compilato nativamente per linux/arm64 (aarch64)**

---

## ⚡ Quick Start

### 1. Trigger il workflow

**Opzione A: Automatico**
```bash
git push origin main
```

**Opzione B: Tag di release**
```bash
git tag v3.10.13
git push origin --tags
```

**Opzione C: Manuale da GitHub**
- Vai su **Actions** → **Build Python 3.10 ARM64 Archive**
- Clicca **Run workflow**
- Opzionalmente specifica la versione di Python

### 2. Scarica l'archivio

L'archivio sarà disponibile in:
- **Artifacts** (link nella run del workflow) - valido 30 giorni
- **Releases** (se hai triggerato con tag)

### 3. Usa in Yocto

```bash
# Estrai
tar -xzf python-arm64.tar.gz -C /opt/

# Verifica
/opt/python-arm64/bin/python3 --version
/opt/python-arm64/bin/pip list
```

Per la guida completa di integrazione con Yocto, vedi **[YOCTO_INTEGRATION.md](YOCTO_INTEGRATION.md)**

---

## 📋 File del repository

| File | Descrizione |
|------|-----------|
| `.github/workflows/build-python-arm64-archive.yml` | Workflow GitHub Actions |
| `Dockerfile.python-arm64` | Dockerfile per la compilazione |
| `YOCTO_INTEGRATION.md` | Guida completa per Yocto |
| `README.md` | Questo file |
| `.gitignore` | Esclusioni git |

---

## 🔧 Personalizzazioni

### Cambiare versione di Python

Nel workflow, modifica:

```yaml
default: '3.10.13'  # Cambia qui
```

O specifica manualmente nel trigger manuale di GitHub.

### Aggiungere/rimuovere package

Modifica il `Dockerfile.python-arm64`:

```dockerfile
RUN /opt/python-arm64/bin/pip install --no-cache-dir \
    numpy \
    opencv-python \
    mss \
    pynput \
    pillow \           # Aggiungi qui
    requests \
```

### Compilare localmente

Se non vuoi usare GitHub Actions:

```bash
# Richiede Docker con supporto multi-platform
docker buildx build \
  --platform linux/arm64 \
  -f Dockerfile.python-arm64 \
  -o type=docker \
  .
```

---

## 📊 Specifiche

| Aspetto | Dettagli |
|---------|----------|
| **Architettura** | linux/arm64 (aarch64) |
| **Python** | 3.10.13 (configurabile) |
| **Base image** | Debian Bookworm (slim) |
| **Dimensione** | ~150-200 MB (compresso) |
| **Build time** | ~10-15 min (dipende da GitHub) |

---

## ⚠️ Requisiti

- Un repository GitHub accessibile
- GitHub Actions abilitato (di default)
- ~500 MB di spazio nel target Yocto per Python estratto

---

## 🆘 Troubleshooting

### Il workflow non parte
- Verifica che GitHub Actions sia abilitato: **Settings → Actions → Allow all actions**
- Controlla che il file sia in `.github/workflows/`

### Build fallisce
- Controlla i log del workflow: **Actions → ultima run → Logs**
- Verifica la sintassi del Dockerfile
- Assicurati che i package siano disponibili su PyPI

### Archivio corrotto
- Scarica nuovamente dall'Artifacts
- Prova con un tag di release più recente

Per aiuto: apri una issue nel repository!

---

## 📚 Risorse utili

- [Documentazione Python](https://www.python.org/downloads/)
- [Yocto Project](https://www.yoctoproject.org/)
- [Docker multi-platform builds](https://docs.docker.com/build/building/multi-platform/)
- [GitHub Actions](https://github.com/features/actions)

---

## 📄 License

Questo repository è fornito come-è. Python è sotto licenza PSF.

---

**Creato per**: Compilazione cross-platform Python ARM64 per dispositivi Yocto  
**Ultimo aggiornamento**: 2026-06-11
