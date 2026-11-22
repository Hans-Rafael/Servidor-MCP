# MCP delegador

Permite que Claude delegue subtareas a Gemini, DeepSeek o Groq.

## Instalación (Linux Mint)

```bash
cd mcp-delegador
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
```

## API keys (nunca dentro del código)

- Gemini: Google AI Studio → `GEMINI_API_KEY`
- DeepSeek: plataforma de DeepSeek → `DEEPSEEK_API_KEY`
- Groq (opcional): consola de Groq → `GROQ_API_KEY`

Verifica en cada sitio los límites y los términos de uso de datos del plan
gratuito antes de enviar información sensible.

## Registrar en Claude Code

```bash
claude mcp add delegador \
  -e GEMINI_API_KEY=tu_clave \
  -e DEEPSEEK_API_KEY=tu_clave \
  -e DELEGADOR_DIR=/ruta/a/tu/proyecto \
  -- /ruta/a/mcp-delegador/.venv/bin/python /ruta/a/mcp-delegador/server.py
```

`DELEGADOR_DIR` limita qué archivos puede leer el servidor.

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
