# Evaluación Técnica Iyata - Automatización y Datos

Este repositorio contiene la solución a la evaluación técnica para el rol de **Desarrollador Junior en Automatización y Datos**.

## Parte A: Workflow de n8n - Renovación de Tokens MercadoLibre

### Objetivo de la Automatización
El objetivo de este flujo es mantener activa la conexión con la API de MercadoLibre mediante la renovación automática del `Access Token`. Dado que estos tokens expiran cada 6 horas, el flujo garantiza la continuidad operativa sin intervención manual.

**Funcionalidades Clave:**
1.  **Lectura y Escritura en Google Sheets:** Obtiene el último token válido y almacena el nuevo tras la renovación.
2.  **Integración API (MercadoLibre):** Realiza la petición POST al endpoint OAuth oficial.
3.  **Agente de IA (Manejo de Errores):** En caso de fallo en la API, un agente de LangChain (OpenAI GPT-4 Mini) analiza el código de error crudo, lo traduce a un lenguaje técnico explicativo y genera una solución accionable.
4.  **Notificaciones:** Alerta inmediata vía Slack con el diagnóstico de la IA.

### 🎥 Video Demo
Puedes ver la explicación del funcionamiento y la ejecución en vivo aquí:
[Ver Video Tutorial en YouTube](https://youtu.be/F92ydQJyZY0)

### Configuración de Credenciales
Para ejecutar este workflow en un entorno local o nube, se requieren configurar las siguientes credenciales en n8n:

1.  **Google Sheets:** Credencial OAuth2 o Service Account con permisos de edición sobre la hoja de destino.
2.  **MercadoLibre API:**
    * En el nodo *Refresh OAuth ML*, se deben ingresar el `Client ID` y `Client Secret` de tu aplicación de MercadoLibre.
    * `Redirect URI`: Debe coincidir con la configurada en tu App de ML.
3.  **OpenAI:** API Key válida para el uso del modelo `gpt-4.1-mini`.
4.  **Slack:** Credencial OAuth para enviar mensajes al canal de auditoría.

### Cómo ejecutar y probar el workflow
1.  Importar el archivo `workflow.json` en n8n.
2.  Crear una hoja de Google Sheets con las columnas: `timestamp`, `access_token`, `refresh_token`, `expires_in`, `user_id`.
3.  Configurar las credenciales en los nodos correspondientes.
4.  Ejecutar manualmente el nodo inicial o esperar al Trigger programado (cada 6 horas).

---

## Parte B: Dashboard de Auditoría de Datos (Google Sheets)

La solución de análisis, limpieza de datos y dashboard de control de calidad se encuentra disponible en el siguiente enlace público:

* 📊 **Ver Solución en Google Sheets:** [Clic aquí para ver el Dashboard](https://docs.google.com/spreadsheets/d/13esaz5DV_fbanQt8b2IaG-kpiFqa3xoBliAfE053gPY/edit?usp=sharing)

> **Nota:** El archivo tiene permisos de lectura públicos para facilitar la revisión.

---

### Autor
Entregado para el proceso de selección de Iyata - 2025.
