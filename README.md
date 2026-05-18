# CNCom · Jurisprudencia

Buscador web estático de boletines de jurisprudencia de la **Cámara Nacional de Apelaciones en lo Comercial** (Poder Judicial de la Nación, Argentina).

**→ [Ver buscador en línea](https://TU-USUARIO.github.io/cncomericial-jurisprudencia/)**

## Qué incluye

- Buscador full-text sobre sumarios, carátulas y texto de fallos
- Filtros por sala (A–F), materia, fecha, expediente, juez y boletín
- Vista de detalle con ficha completa de cada fallo
- 100% estático: funciona sin servidor, sin base de datos paga

## Estructura del repo

```
├── index.html          ← app web (abrir en cualquier browser o GitHub Pages)
├── data/
│   └── fallos.json     ← base de datos generada (no editar manualmente)
├── raw/
│   └── Bol_2-2026.pdf  ← PDFs originales archivados
└── scripts/
    └── parse_boletin.py ← parser: PDF → fallos.json
```

## Agregar un nuevo boletín

**Requisitos:** Python 3.10+, poppler-utils (`apt install poppler-utils`)

```bash
# 1. Copiar el PDF a raw/
cp ~/Downloads/Bol_3-2026.pdf raw/

# 2. Parsear y actualizar la base
python scripts/parse_boletin.py raw/Bol_3-2026.pdf

# 3. Commitear (data/fallos.json + raw/Bol_3-2026.pdf)
git add data/fallos.json raw/Bol_3-2026.pdf
git commit -m "Agrega Boletín 3 - 2026"
git push
```

La web se actualiza sola en GitHub Pages (suele tardar 1-2 minutos).

## Parsear múltiples boletines de una vez

```bash
python scripts/parse_boletin.py raw/Bol_*.pdf
```

El script detecta automáticamente duplicados y solo agrega fallos nuevos.

## Despliegue inicial en GitHub Pages

1. Crear repo en GitHub (puede ser público o privado con Pages habilitado)
2. Subir todos los archivos:
   ```bash
   git init
   git remote add origin https://github.com/TU-USUARIO/cncomericial-jurisprudencia.git
   git add .
   git commit -m "Versión inicial"
   git push -u origin main
   ```
3. En GitHub → Settings → Pages → Source: `main` / `/ (root)`
4. La URL será: `https://TU-USUARIO.github.io/cncomericial-jurisprudencia/`

## Dependencias del parser

```bash
# Ubuntu/Debian
sudo apt install poppler-utils python3

# macOS
brew install poppler
```

No se requieren librerías Python adicionales (solo stdlib).

## Licencia

Datos: © Poder Judicial de la Nación Argentina. Código: MIT.
