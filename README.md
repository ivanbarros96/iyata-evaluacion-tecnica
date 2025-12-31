# Evaluación Técnica Iyata - Automatización y Datos

Este repositorio contiene la solución a la evaluación técnica para el rol de **Desarrollador Junior en Automatización y Datos**.

## Parte A: Workflow de n8n - Renovación de Tokens MercadoLibre

### 🎯 Objetivo de la Automatización
**El Problema:** La API de MercadoLibre utiliza tokens de acceso (`access_token`) que caducan cada 6 horas. Si no se renuevan a tiempo, las integraciones de venta y stock dejan de funcionar, causando pérdidas operativas.

**La Solución:** Este workflow automatiza el ciclo de vida de la autenticación mediante:
1.  **Renovación Proactiva:** Un trigger programado renueva el token antes de que expire.
2.  **Persistencia de Datos:** Lee el último `refresh_token` válido desde Google Sheets y guarda el nuevo generado.
3.  **Resiliencia con IA:** Integra un agente de **OpenAI (GPT-4 Mini)** que, en caso de fallo en la API, analiza el código de error técnico y envía un diagnóstico claro y accionable en español a Slack.

### 🎥 Video Demo
Explicación detallada del flujo y pruebas:
[Ver Video Tutorial en YouTube](https://youtu.be/F92ydQJyZY0)

### 🔐 Configuración de Credenciales
Para desplegar este proyecto, se deben configurar las siguientes credenciales en el gestor de credenciales de n8n:

1.  **Google Sheets (OAuth2):**
    * Requiere una cuenta de Google Cloud Console con la API de Sheets habilitada.
    * Scopes necesarios: `drive.file` o `spreadsheets`.
2.  **MercadoLibre (HTTP Request):**
    * En el nodo *Refresh OAuth ML*, se deben ingresar manualmente:
        * `Client ID` (App ID de MercadoLibre).
        * `Client Secret` (Secret Key).
        * `Redirect URI` (Debe coincidir con la configuración de tu App).
3.  **OpenAI (API Key):**
    * Configurar una credencial tipo "OpenAI API" con una Key válida que tenga acceso al modelo `gpt-4.1-mini` (o superior).
4.  **Slack (OAuth2):**
    * Configurar la conexión con un Workspace y seleccionar el canal destino (en este caso, `#auditoria-agentes-ia`).

### 🚀 Cómo ejecutar y probar el workflow
1.  **Importación:** Descarga el archivo `workflow.json` de este repositorio e impórtalo en n8n (Menú "Import from File").
2.  **Preparación de Datos:** Crea una hoja de Google Sheets vacía con los encabezados: `timestamp`, `access_token`, `refresh_token`, `expires_in`, `user_id`. Agrega una primera fila con datos semilla (o datos ficticios) para la primera lectura.
3.  **Conexión:** Asigna tus credenciales configuradas a los nodos correspondientes (Sheets, OpenAI, Slack).
4.  **Prueba Manual:**
    * Haz clic en el botón **"Test Workflow"** (o ejecuta manualmente el nodo *Trigger*).
    * Verifica que se cree una nueva fila en Google Sheets con el token actualizado.
5.  **Prueba de Error (Opcional):** Para probar el agente de IA, altera intencionalmente el `Client Secret` en el nodo HTTP y ejecuta de nuevo. Deberías recibir una alerta explicativa en Slack.

---

## Parte B: Dashboard de Auditoría de Datos (Google Sheets)

La solución de análisis, limpieza de datos y dashboard de control de calidad se encuentra disponible en el siguiente enlace público:

* 📊 **Ver Solución en Google Sheets:** [Clic aquí para ver el Dashboard](https://docs.google.com/spreadsheets/d/13esaz5DV_fbanQt8b2IaG-kpiFqa3xoBliAfE053gPY/edit?usp=sharing)

> **Nota:** El archivo tiene permisos de lectura públicos para facilitar la revisión.

---

### Autor
Entregado por **Ivan Barros** para el proceso de selección de Iyata - 2025.
