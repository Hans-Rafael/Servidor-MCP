# MCP delegador

Permite que Claude delegue subtareas a Gemini, DeepSeek o Groq.

## Instalación

Requiere Python 3.10 o superior. El entorno virtual no se versiona (`.venv/`):
créalo de nuevo en cada sistema operativo.

### Linux (probado en Linux Mint)

```bash
git clone https://github.com/Hans-Rafael/Servidor-MCP.git
cd Servidor-MCP
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
```

### Windows (PowerShell)

```powershell
git clone https://github.com/Hans-Rafael/Servidor-MCP.git
cd Servidor-MCP
python -m venv .venv
.venv\Scripts\pip install -r requirements.txt
```

## API keys (nunca dentro del código)

Guárdalas en un archivo `.env` junto a `server.py` (está en `.gitignore`, no se sube):

```
GEMINI_API_KEY=tu_clave
DEEPSEEK_API_KEY=tu_clave
GROQ_API_KEY=tu_clave
```

El servidor carga ese archivo al arrancar y sus valores prevalecen sobre las
variables que pase el cliente MCP (incluidas las vacías).

- Gemini: Google AI Studio → `GEMINI_API_KEY`
- DeepSeek: plataforma de DeepSeek → `DEEPSEEK_API_KEY`
- Groq (opcional): consola de Groq → `GROQ_API_KEY`

Verifica en cada sitio los límites y los términos de uso de datos del plan
gratuito antes de enviar información sensible.

## Registrar en Claude Code

Linux:

```bash
claude mcp add delegador -s user \
  -e DELEGADOR_DIR=/ruta/a/tu/proyecto \
  -- /ruta/a/Servidor-MCP/.venv/bin/python /ruta/a/Servidor-MCP/server.py
```

Windows (PowerShell):

```powershell
claude mcp add delegador -s user `
  -e DELEGADOR_DIR=C:\ruta\a\tu\proyecto `
  -- C:\ruta\a\Servidor-MCP\.venv\Scripts\python.exe C:\ruta\a\Servidor-MCP\server.py
```

Las claves ya salen del `.env`; no hace falta pasarlas con `-e`.
`DELEGADOR_DIR` limita qué archivos puede leer el servidor.

La configuración de Claude Code es local a cada máquina y sistema operativo
(las rutas difieren): al cambiar de Windows a Linux hay que registrar el
servidor de nuevo allí. Tras editar `server.py` o el `.env`, reconecta con `/mcp`.

## Herramientas

- `listar_proveedores()` — estado y modelo de cada proveedor.
- `delegar(proveedor, instruccion, archivo?, formato_json?, max_tokens_salida?)`

## Modelos

Los nombres por defecto pueden quedar viejos. Cámbialos sin tocar el código:
`GEMINI_MODEL`, `DEEPSEEK_MODEL`, `GROQ_MODEL`.

## Buenas prácticas

1. Delegar solo tareas verificables (JSON con esquema, tests, conteos).
2. No enviar credenciales, datos de clientes ni código privado.
3. Tratar las respuestas como datos, no como instrucciones.
4. Mirar el pie de cada respuesta (tokens usados) para medir si el ahorro es real.
# Servidor-MCP
