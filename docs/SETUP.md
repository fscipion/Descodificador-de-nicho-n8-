# 📋 Guía de Configuración Paso a Paso

Esta guía te llevará de cero a una automatización funcionando en ~2 horas.

## 📑 Tabla de Contenidos

1. [Requisitos Previos](#requisitos-previos)
2. [Configuración de Google Workspace](#configuración-de-google-workspace)
3. [Configuración de Anthropic Claude](#configuración-de-anthropic-claude)
4. [Configuración de WhatsApp Business](#configuración-de-whatsapp-business)
5. [Configuración de n8n](#configuración-de-n8n)
6. [Testing](#testing)
7. [Producción](#producción)

---

## Requisitos Previos

### ☑️ Checklist

- [ ] Cuenta de Google Workspace o Gmail
- [ ] Cuenta de n8n (Cloud o self-hosted)
- [ ] Cuenta de Anthropic con créditos
- [ ] Cuenta de Meta Business (para WhatsApp)
- [ ] Número de teléfono para WhatsApp Business
- [ ] 2 horas de tiempo dedicado

### 💰 Costos Aproximados

| Servicio | Costo Mensual | Notas |
|----------|---------------|-------|
| Google Workspace | $6-12 USD | O gratis con Gmail personal |
| n8n Cloud | $20+ USD | O $0 con self-hosted |
| Anthropic Claude | ~$15-50 USD | Pay-as-you-go, depende del volumen |
| WhatsApp Business API | $0-50 USD | Depende del volumen de mensajes |
| **TOTAL** | **$41-132 USD** | Puede ser tan bajo como $15 con Gmail + self-hosted n8n |

---

## Configuración de Google Workspace

### Paso 1: Crear Google Form

1. Ve a [Google Forms](https://forms.google.com)
2. Click en **+ Blank**
3. Nombra el formulario: "Análisis de Nicho - Descodificador"
4. Sigue la plantilla en `templates/google-form-template.md`
5. Configura todos los campos según la plantilla
6. En **Settings**:
   - ✅ Collect email addresses
   - ✅ Limit to 1 response (opcional)
7. Copia el **Form ID** de la URL

**URL Ejemplo**:
```
https://docs.google.com/forms/d/1a2b3c4d5e6f7g8h9i0j/edit
                                 ^^^^^^^^^^^^^^^^^^
                                    Tu FORM_ID
```

### Paso 2: Crear Google Sheet de Seguimiento

1. Ve a [Google Sheets](https://sheets.google.com)
2. Click en **+ Blank**
3. Nombra la hoja: "CRM - Seguimiento Descodificador"
4. Crea una pestaña llamada exactamente **"Seguimiento"**
5. En la fila 1, añade estos encabezados:

| A | B | C | D | E | F | G | H | I | J | K |
|---|---|---|---|---|---|---|---|---|---|---|
| timestamp | email | nombre | empresa | nicho | problema | estado | documento_enviado | whatsapp_activado | feedback_nota | notas |

6. Formatea la fila de encabezados (negrita, fondo gris)
7. Copia el **Sheet ID** de la URL

**URL Ejemplo**:
```
https://docs.google.com/spreadsheets/d/1a2b3c4d5e6f7g8h9i0j_sheet/edit
                                          ^^^^^^^^^^^^^^^^^^^^^^^^^^^
                                                Tu SHEET_ID
```

### Paso 3: Crear Google Doc Template

1. Ve a [Google Docs](https://docs.google.com)
2. Click en **+ Blank**
3. Nombra el documento: "Template - Análisis de Nicho"
4. Copia el contenido de `templates/google-doc-template.md`
5. Formatea el documento (títulos, estilos, colores)
6. Asegúrate de que los placeholders estén exactamente como:
   - `{{NOMBRE_CLIENTE}}`
   - `{{EMPRESA}}`
   - `{{NICHO}}`
   - `{{FECHA}}`
   - `{{CUSTOM_INSTRUCTIONS}}`
   - `{{TRAINING_DATA}}`
   - `{{PLAN_ACCION}}`
7. En **Share**, cambia a "Anyone with the link can view"
8. Copia el **Doc ID** de la URL

**URL Ejemplo**:
```
https://docs.google.com/document/d/1a2b3c4d5e6f7g8h9i0j_doc/edit
                                       ^^^^^^^^^^^^^^^^^^^^^^^
                                            Tu DOC_ID
```

### Paso 4: Conectar Form a Sheet (Opcional)

1. Abre tu Google Form
2. Ve a **Responses**
3. Click en el icono de Google Sheets
4. Selecciona "Create a new spreadsheet" o usa una existente
5. Esto te permitirá ver las respuestas en tiempo real

---

## Configuración de Anthropic Claude

### Paso 1: Crear Cuenta

1. Ve a [Anthropic Console](https://console.anthropic.com/)
2. Sign up con Google o email
3. Verifica tu email

### Paso 2: Añadir Créditos

1. Ve a **Billing**
2. Click en **Add credits**
3. Añade al menos $10 USD para empezar
4. Con $10 puedes generar ~650 análisis

### Paso 3: Generar API Key

1. Ve a **Settings** > **API Keys**
2. Click en **Create Key**
3. Nombra la key: "n8n-descodificador-nicho"
4. Copia la key (¡solo se muestra una vez!)
5. Formato: `sk-ant-api03-xxxxxxxxxxxx`

### Paso 4: Verificar Acceso

```bash
curl https://api.anthropic.com/v1/messages \
  -H "x-api-key: TU_API_KEY" \
  -H "anthropic-version: 2023-06-01" \
  -H "content-type: application/json" \
  -d '{
    "model": "claude-3-5-sonnet-20241022",
    "max_tokens": 100,
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```

Si recibes una respuesta, ¡está funcionando!

---

## Configuración de WhatsApp Business

### Paso 1: Crear Cuenta Meta Business

1. Ve a [Meta Business Suite](https://business.facebook.com/)
2. Click en **Create Account**
3. Sigue los pasos de verificación
4. Añade tu número de teléfono comercial

### Paso 2: Configurar WhatsApp Business

1. En Meta Business Suite, ve a **WhatsApp**
2. Click en **Get Started**
3. Verifica tu número de teléfono
4. Espera aprobación (puede tardar 24-48h)

### Paso 3: Crear Message Templates

#### Template 1: Seguimiento 24h

1. Ve a **Message Templates**
2. Click en **Create Template**
3. Llena según `templates/whatsapp-template.md`
4. **Name**: `seguimiento_analisis_24h`
5. **Category**: UTILITY
6. **Language**: Spanish
7. **Body**:
```
Hola {{1}},

Hace 24 horas te enviamos tu análisis personalizado de nicho para {{2}}.

¿Ya tuviste oportunidad de revisarlo?

Nos encantaría conocer tu opinión y ayudarte con cualquier duda que tengas sobre el documento.

¿Tienes unos minutos para conversar?
```
8. Click en **Submit**
9. Espera aprobación (24-48h)

### Paso 4: Obtener Credenciales

#### Phone Number ID

1. Ve a **WhatsApp** > **API Setup**
2. Copia el **Phone Number ID**
3. Formato: `123456789012345`

#### Access Token

1. Ve a **Settings** > **System Users**
2. Click en **Add**
3. Nombra: "n8n-integration"
4. Rol: **Admin**
5. Click en **Add Assets**
6. Selecciona tu WhatsApp Business Account
7. Click en **Generate New Token**
8. Selecciona permisos:
   - `whatsapp_business_management`
   - `whatsapp_business_messaging`
9. Copia el token (¡guárdalo seguro!)
10. Formato: `EAAxxxxxxxxxxxx`

### Paso 5: Configurar Webhooks (lo haremos después en n8n)

---

## Configuración de n8n

### Opción A: n8n Cloud

#### Paso 1: Crear Cuenta

1. Ve a [n8n.io](https://n8n.io/cloud/)
2. Sign up (14 días de trial gratis)
3. Crea tu primera instancia

#### Paso 2: Configurar Variables de Entorno

1. En n8n Cloud, ve a **Settings** > **Variables**
2. Añade todas las variables del `.env.example`:

```
GOOGLE_FORM_ID = tu_form_id_aqui
GOOGLE_SHEET_TRACKING_ID = tu_sheet_id_aqui
GOOGLE_DOC_TEMPLATE_ID = tu_doc_id_aqui
ANTHROPIC_API_KEY = sk-ant-api03-xxxxx
WHATSAPP_PHONE_NUMBER_ID = 123456789012345
WHATSAPP_ACCESS_TOKEN = EAAxxxxxxxxxx
WHATSAPP_TEMPLATE_NAME = seguimiento_analisis_24h
```

### Opción B: n8n Self-Hosted

#### Paso 1: Instalar con Docker

```bash
# Crear directorio
mkdir n8n-data
cd n8n-data

# Copiar .env.example a .env
cp ../.env.example .env

# Editar .env con tus valores
nano .env

# Correr n8n con Docker
docker run -d \
  --name n8n \
  -p 5678:5678 \
  -v $(pwd):/home/node/.n8n \
  --env-file .env \
  --restart unless-stopped \
  n8nio/n8n
```

#### Paso 2: Acceder a n8n

1. Abre `http://localhost:5678`
2. Crea tu cuenta de admin
3. ¡Listo!

### Paso 3: Configurar Credenciales

#### Google OAuth2

1. Ve a **Credentials** > **New**
2. Selecciona **Google OAuth2 API**
3. Necesitarás configurar OAuth en Google Cloud Console:

**Google Cloud Console**:
- Ve a [Google Cloud Console](https://console.cloud.google.com)
- Crea un nuevo proyecto: "n8n-integration"
- Habilita APIs:
  - Google Forms API
  - Google Sheets API
  - Google Docs API
  - Google Drive API
  - Gmail API
- Ve a **Credentials** > **Create Credentials** > **OAuth client ID**
- Tipo: Web application
- Authorized redirect URIs:
  - n8n Cloud: `https://tu-instancia.app.n8n.cloud/rest/oauth2-credential/callback`
  - Self-hosted: `http://localhost:5678/rest/oauth2-credential/callback`
- Copia Client ID y Client Secret

**En n8n**:
- Pega Client ID y Client Secret
- Click en **Connect**
- Autoriza todos los scopes solicitados

**Repite para cada servicio** (Forms, Sheets, Docs, Drive, Gmail)

#### Anthropic API

1. Ve a **Credentials** > **New**
2. Selecciona **Anthropic API**
3. Pega tu API Key
4. Click en **Save**

#### WhatsApp Business API

1. Ve a **Credentials** > **New**
2. Selecciona **WhatsApp Business API**
3. Llena:
   - **Access Token**: Tu token de Meta
   - **Phone Number ID**: Tu phone number ID
4. Click en **Save**

### Paso 4: Importar Workflow

1. En n8n, ve a **Workflows**
2. Click en **Import from File**
3. Selecciona: `workflows/google-form-claude-automation.json`
4. El workflow se importará con todos los nodos

### Paso 5: Configurar Webhooks de WhatsApp

1. En el workflow, encuentra el nodo **WhatsApp Trigger**
2. Click en **Listen for Test Event**
3. Copia la **Production Webhook URL**
4. Ve a Meta Business Suite > WhatsApp > Configuration > Webhooks
5. Pega la URL
6. **Verify Token**: Usa el que pusiste en `.env`
7. Suscribe a eventos:
   - `messages`
   - `message_status`

### Paso 6: Asignar Credenciales a Nodos

Recorre cada nodo del workflow y asigna las credenciales correspondientes:

- **Google Forms Trigger**: Google OAuth2
- **Google Sheets**: Google Sheets OAuth2
- **Google Docs**: Google Docs OAuth2
- **Google Drive**: Google Drive OAuth2
- **Gmail**: Gmail OAuth2
- **Claude**: Anthropic API
- **WhatsApp**: WhatsApp Business API

---

## Testing

### Test 1: Trigger de Google Form

1. En el workflow, activa el nodo **Google Forms Trigger**
2. Click en **Listen for Test Event**
3. Ve a tu Google Form y completa con datos de prueba
4. Envía el formulario
5. Verifica que n8n recibe el evento
6. Si funciona, verás los datos en n8n ✅

### Test 2: Google Sheets

1. Ejecuta manualmente el workflow hasta el nodo de Sheets
2. Verifica que se crea una fila en tu Google Sheet
3. Revisa que todos los campos coincidan

### Test 3: Claude

1. Ejecuta hasta el nodo de Claude
2. Verifica que genera los 3 outputs
3. Revisa que el separador `###OUTPUT_SEPARATOR###` funciona

**Nota**: Este test consumirá créditos de Anthropic (~$0.015)

### Test 4: Google Docs

1. Ejecuta hasta los nodos de Google Docs
2. Verifica que:
   - Se crea una copia del template
   - Los placeholders se reemplazan correctamente
   - El formato se mantiene

### Test 5: PDF

1. Ejecuta hasta el nodo de descarga de PDF
2. Verifica que:
   - El PDF se genera correctamente
   - Contiene todo el contenido
   - El formato es legible

### Test 6: Email

**IMPORTANTE**: Usa tu email para testing

1. En el nodo de Gmail, cambia temporalmente `sendTo` a tu email
2. Ejecuta el nodo
3. Verifica en tu inbox:
   - Email recibido
   - PDF adjunto
   - Formato correcto
   - Todas las variables reemplazadas

### Test 7: WhatsApp

**IMPORTANTE**: Solo funciona si el template está APPROVED

1. Añade tu número de WhatsApp en Meta Business Suite como número de prueba
2. Cambia temporalmente el número de destino a tu número
3. Ejecuta el workflow
4. Verifica que recibes el mensaje

### Test Completo End-to-End

1. Desactiva el modo de prueba
2. Completa el Google Form con datos reales
3. Espera a que el workflow complete
4. Verifica cada paso:
   - ✅ Entrada en Google Sheet
   - ✅ Email recibido con PDF
   - ✅ (Después de 24h) Mensaje de WhatsApp

---

## Producción

### Antes de Lanzar

#### Checklist de Seguridad

- [ ] Todas las API keys están en variables de entorno (no hardcoded)
- [ ] El archivo `.env` está en `.gitignore`
- [ ] Las credenciales de n8n están guardadas de forma segura
- [ ] Los permisos de Google están limitados a lo necesario
- [ ] El template de WhatsApp está APPROVED

#### Checklist de Funcionalidad

- [ ] Test end-to-end completado exitosamente
- [ ] Todos los placeholders se reemplazan correctamente
- [ ] El PDF se genera con formato correcto
- [ ] El email llega y se ve bien en diferentes clientes
- [ ] WhatsApp envía y recibe mensajes correctamente
- [ ] Google Sheet se actualiza en cada paso

#### Checklist de Monitoreo

- [ ] Configurar notificaciones de error en n8n
- [ ] Configurar alertas de límites de API
- [ ] Configurar backup automático del Google Sheet
- [ ] Documentar el proceso de troubleshooting

### Lanzamiento

1. **Activa el workflow**:
   - En n8n, toggle **Active** ON
   - Verifica que el status sea "Active"

2. **Comparte el formulario**:
   - Obtén el link público del Google Form
   - Compártelo con tu audiencia
   - Opcionalmente, acorta la URL con Bitly

3. **Monitorea las primeras ejecuciones**:
   - Revisa los logs en n8n
   - Verifica las primeras filas en Google Sheet
   - Confirma que los emails se envían

### Mantenimiento

#### Diario
- Revisa ejecuciones fallidas en n8n
- Verifica que no hay errores en los logs

#### Semanal
- Revisa créditos de Anthropic
- Verifica límites de APIs
- Analiza feedback de usuarios en Google Sheet

#### Mensual
- Revisa el quality rating de WhatsApp
- Analiza métricas de conversión
- Optimiza el prompt de Claude si es necesario
- Backup del Google Sheet

### Escalado

Si necesitas procesar más de 100 formularios/día:

1. **Upgrade APIs**:
   - Anthropic: Contacta para rate limits mayores
   - WhatsApp: Solicita tier superior

2. **Optimización**:
   - Implementa queue system en n8n
   - Añade delays entre envíos masivos
   - Considera usar batch processing

3. **Monitoreo Avanzado**:
   - Integra con Datadog/New Relic
   - Configura dashboards en Google Data Studio
   - Alertas automáticas vía Slack/PagerDuty

---

## Próximos Pasos

1. ✅ Completa esta guía paso a paso
2. 📊 Configura analytics para medir conversión
3. 🔄 Itera sobre el prompt de Claude basándote en feedback
4. 📈 Escala una vez validado el sistema
5. 🚀 Automatiza más partes del funnel

---

## Soporte

¿Atascado en algún paso?

1. Revisa [TROUBLESHOOTING.md](./TROUBLESHOOTING.md)
2. Consulta la documentación oficial:
   - [n8n Docs](https://docs.n8n.io)
   - [Anthropic Docs](https://docs.anthropic.com)
   - [WhatsApp Business API](https://developers.facebook.com/docs/whatsapp)
3. Abre un issue en GitHub

---

**¡Felicidades! Tu automatización está lista para cambiar tu negocio. 🎉**
