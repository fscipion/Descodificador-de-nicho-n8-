# 🚀 Descodificador de Nicho - Automatización n8n

Automatización completa que convierte respuestas de Google Forms en análisis personalizados usando Claude AI, generando documentos PDF y enviándolos por email con seguimiento por WhatsApp.

## 📋 Descripción del Workflow

Este workflow automatiza todo el proceso de análisis de nicho desde que un usuario completa un formulario hasta el seguimiento por WhatsApp:

1. **Trigger**: Nueva entrada en Google Forms
2. **Registro**: Actualiza Google Sheets con la información del usuario
3. **Análisis IA**: Claude genera 3 outputs personalizados:
   - Custom Instructions para el nicho
   - Training Data con casos de éxito
   - Plan de Acción de 30 días
4. **Documento**: Integra las respuestas de Claude en una plantilla de Google Docs
5. **PDF**: Descarga el documento personalizado como PDF
6. **Email**: Envía el PDF al usuario vía Gmail
7. **Seguimiento**: Después de 24h, envía mensaje por WhatsApp
8. **Feedback**: Captura la respuesta del usuario y solicita valoración 0-10
9. **Actualización**: Registra todo el proceso en Google Sheets

## 🎯 Características

- ✅ Integración completa con Google Workspace (Forms, Sheets, Docs, Drive, Gmail)
- ✅ IA Generativa con Claude 3.5 Sonnet
- ✅ Generación automática de documentos PDF personalizados
- ✅ Sistema de seguimiento por WhatsApp con templates aprobados
- ✅ Mini CRM en Google Sheets para tracking completo
- ✅ Validación de feedback con notas 0-10
- ✅ Mensajes programados con delay de 24 horas

## 🔧 Requisitos Previos

### 1. Cuenta n8n
- n8n Cloud o instalación self-hosted
- Versión n8n >= 1.0

### 2. APIs y Credenciales

#### Google Workspace
- Cuenta de Google con acceso a:
  - Google Forms
  - Google Sheets
  - Google Docs
  - Google Drive
  - Gmail
- OAuth2 configurado para cada servicio

#### Anthropic Claude
- API Key de Anthropic
- Acceso a Claude 3.5 Sonnet
- Créditos disponibles

#### Meta WhatsApp Business
- WhatsApp Business API
- Phone Number ID verificado
- Templates de mensaje aprobados por Meta
- Access Token de la API

## 📦 Instalación

### Paso 1: Clonar el Repositorio

```bash
git clone https://github.com/tu-usuario/Descodificador-de-nicho-n8-.git
cd Descodificador-de-nicho-n8-
```

### Paso 2: Configurar Variables de Entorno

Crea un archivo `.env` basándote en `.env.example`:

```bash
cp .env.example .env
```

Edita el archivo `.env` con tus credenciales (ver sección Configuración).

### Paso 3: Importar Workflow a n8n

1. Accede a tu instancia de n8n
2. Ve a **Workflows** > **Import**
3. Selecciona el archivo: `workflows/google-form-claude-automation.json`
4. El workflow se importará con todos los nodos configurados

### Paso 4: Configurar Credenciales en n8n

Configura las siguientes credenciales en n8n:

#### Google APIs
1. Ve a **Settings** > **Credentials** > **New**
2. Selecciona **Google OAuth2 API**
3. Configura para cada servicio:
   - Google Forms
   - Google Sheets
   - Google Docs
   - Google Drive
   - Gmail

[Ver guía detallada de OAuth2 de Google](https://docs.n8n.io/integrations/builtin/credentials/google/)

#### Anthropic API
1. Credential Type: **Anthropic API**
2. API Key: Tu clave de Anthropic

#### WhatsApp Business API
1. Credential Type: **WhatsApp Business API**
2. Access Token: Token de Meta
3. Phone Number ID: ID de tu número de WhatsApp Business

## ⚙️ Configuración

### Variables de Entorno

Configura estas variables en n8n (Settings > Variables):

```
GOOGLE_FORM_ID=tu-formulario-id
GOOGLE_SHEET_TRACKING_ID=tu-sheet-id
GOOGLE_DOC_TEMPLATE_ID=tu-plantilla-doc-id
WHATSAPP_PHONE_NUMBER_ID=tu-phone-number-id
WHATSAPP_TEMPLATE_NAME=nombre-template-aprobado
```

### Configurar Google Form

Tu formulario debe incluir estos campos (nombres exactos):

- `timestamp` (automático)
- `email` (Email address)
- `nombre` (Short answer)
- `empresa` (Short answer)
- `nicho` (Short answer)
- `problema` (Paragraph)
- `objetivos` (Paragraph)
- `audiencia` (Paragraph)
- `competencia` (Paragraph)
- `telefono` (Short answer) - Formato: +34XXXXXXXXX

### Configurar Google Sheets

Crea una hoja llamada "Seguimiento" con estas columnas:

| A | B | C | D | E | F | G | H | I | J | K |
|---|---|---|---|---|---|---|---|---|---|---|
| timestamp | email | nombre | empresa | nicho | problema | estado | documento_enviado | whatsapp_activado | feedback_nota | notas |

### Configurar Google Docs Template

Tu plantilla debe incluir estos placeholders:

```
{{NOMBRE_CLIENTE}}
{{EMPRESA}}
{{NICHO}}
{{FECHA}}

Sección 1: Custom Instructions
{{CUSTOM_INSTRUCTIONS}}

Sección 2: Training Data
{{TRAINING_DATA}}

Sección 3: Plan de Acción
{{PLAN_ACCION}}
```

### Configurar WhatsApp Template

Crea un template en Meta Business Suite con:

**Nombre**: `seguimiento_24h` (o el que prefieras)

**Categoría**: MARKETING

**Idioma**: Español

**Contenido**:
```
Hola {{1}},

¿Recibiste nuestro análisis de nicho?

Nos encantaría conocer tu opinión y ayudarte con cualquier duda que tengas.

¿Tienes unos minutos para conversar?
```

**Variables**:
- {{1}} = Nombre del cliente

## 🎮 Uso

### Activar el Workflow

1. En n8n, abre el workflow importado
2. Verifica que todos los nodos estén correctamente configurados
3. Click en **Active** (toggle superior derecho)
4. El workflow estará escuchando nuevas entradas del formulario

### Flujo del Usuario

1. **Usuario completa** el Google Form
2. **Automáticamente**:
   - Se registra en Google Sheets
   - Claude analiza las respuestas
   - Se genera un Google Doc personalizado
   - Se descarga como PDF
   - Se envía por email
3. **24 horas después**:
   - Usuario recibe mensaje de WhatsApp
   - Si responde, se le pregunta feedback (nota 0-10)
   - La nota se registra en Google Sheets

### Monitoreo

Puedes monitorear la ejecución en:

- **n8n**: Executions tab
- **Google Sheets**: Columna "estado" muestra el progreso
- **WhatsApp**: Meta Business Suite > Mensajes

## 🏗️ Estructura del Proyecto

```
Descodificador-de-nicho-n8-/
├── workflows/
│   └── google-form-claude-automation.json    # Workflow completo de n8n
├── templates/
│   ├── google-form-template.md               # Estructura del formulario
│   ├── google-doc-template.md                # Plantilla del documento
│   ├── email-template.md                     # Plantilla del email
│   └── whatsapp-template.md                  # Template de WhatsApp
├── docs/
│   ├── SETUP.md                              # Guía de configuración detallada
│   ├── TROUBLESHOOTING.md                    # Solución de problemas
│   └── API-LIMITS.md                         # Límites de las APIs
├── .env.example                              # Ejemplo de variables de entorno
└── README.md                                 # Esta documentación
```

## 🔍 Detalles Técnicos

### Nodos del Workflow

| Nodo | Tipo | Función |
|------|------|---------|
| Google Forms Trigger | Trigger | Detecta nuevas entradas del formulario |
| Actualizar Google Sheet - Registro Inicial | Google Sheets | Registra la entrada inicial |
| Claude - Generar 3 Outputs | Anthropic Claude | Genera análisis personalizado |
| Separar Outputs de Claude | Code | Parsea los 3 outputs de Claude |
| Google Docs - Copiar Plantilla | Google Drive | Crea copia del template |
| Google Docs - Reemplazar Texto | Google Docs | Inserta datos personalizados |
| Google Drive - Descargar como PDF | Google Drive | Convierte Doc a PDF |
| Gmail - Enviar Documento | Gmail | Envía email con PDF adjunto |
| Esperar 24 Horas | Wait | Delay de 24 horas |
| WhatsApp - Enviar Mensaje 24h | WhatsApp | Mensaje de seguimiento |
| Actualizar Google Sheet - Envío Completado | Google Sheets | Actualiza tracking |
| WhatsApp - Recibir Respuesta | WhatsApp Trigger | Captura respuesta del usuario |
| WhatsApp - Preguntar Feedback | WhatsApp | Solicita nota 0-10 |
| WhatsApp - Recibir Nota Feedback | WhatsApp Trigger | Captura la nota |
| Validar Nota (0-10) | IF | Valida formato de la nota |
| Actualizar Google Sheet - Feedback | Google Sheets | Registra feedback |
| WhatsApp - Agradecer Feedback | WhatsApp | Mensaje de agradecimiento |

### Prompt de Claude

El prompt está diseñado para generar exactamente 3 outputs separados:

1. **Custom Instructions** (máx 800 palabras)
   - Tono y estilo de comunicación
   - Palabras clave del sector
   - Ángulos de diferenciación
   - Errores a evitar

2. **Training Data** (máx 1000 palabras)
   - Casos de éxito similares
   - Framework de análisis
   - Plantillas de mensajes
   - Métricas clave

3. **Plan de Acción** (máx 800 palabras)
   - Acciones semana 1-2
   - Acciones semana 3-4
   - Quick wins
   - KPIs a monitorizar

### Manejo de Errores

El workflow incluye:

- Validación de formato de feedback (regex 0-10)
- Retry automático en caso de fallo de API
- Logs detallados en cada nodo
- Fallback en caso de error de Claude

## 🚨 Solución de Problemas

### El workflow no se activa

- Verifica que el trigger de Google Forms esté activo
- Comprueba los permisos de OAuth2
- Revisa que el Form ID sea correcto

### Claude no genera los 3 outputs

- Verifica que tienes créditos en tu cuenta de Anthropic
- Comprueba que la API Key sea válida
- Revisa el prompt en el nodo de Claude

### El PDF no se genera correctamente

- Asegúrate de que la plantilla de Google Docs existe
- Verifica los permisos de Google Drive
- Comprueba que los placeholders coincidan exactamente

### WhatsApp no envía mensajes

- El template debe estar APROBADO por Meta
- Verifica el Phone Number ID
- El número del usuario debe tener formato internacional (+34...)
- Solo puedes enviar templates si el usuario no ha iniciado conversación

### El Google Sheet no se actualiza

- Verifica el Sheet ID
- Comprueba que la hoja se llame exactamente "Seguimiento"
- Revisa los permisos de la API de Google Sheets

## 📊 Límites de las APIs

### Anthropic Claude
- Rate limit: 50 requests/min
- Tokens: 4000 max por request (configurado)
- Costo: ~$0.015 por request (Claude 3.5 Sonnet)

### Google APIs
- Forms: Sin límite específico
- Sheets: 500 requests/100 segundos/usuario
- Docs: 300 requests/60 segundos/usuario
- Drive: 1000 requests/100 segundos/usuario
- Gmail: 100 requests/segundo/usuario

### WhatsApp Business
- Marketing messages: 1000/día (depende de tu tier)
- Templates: Deben estar pre-aprobados
- Conversaciones: 24h window después de respuesta del usuario

## 🔐 Seguridad

- **Nunca** compartas tus API keys públicamente
- Usa variables de entorno para credenciales sensibles
- Revisa regularmente los permisos de OAuth2
- Implementa rate limiting si esperas alto volumen
- Haz backups regulares de tu Google Sheet

## 🎯 Próximas Mejoras

- [ ] Dashboard de métricas con Google Data Studio
- [ ] A/B testing de prompts de Claude
- [ ] Integración con CRM (HubSpot/Salesforce)
- [ ] Notificaciones a Slack para el equipo
- [ ] Versión multiidioma
- [ ] Análisis de sentimiento del feedback
- [ ] Sistema de puntuación de leads

## 📝 Licencia

MIT License - Siéntete libre de usar y modificar este workflow.

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Por favor:

1. Fork el repositorio
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📧 Soporte

Si tienes problemas o preguntas:

1. Revisa la sección de Troubleshooting
2. Consulta la documentación de n8n: https://docs.n8n.io
3. Abre un issue en GitHub

## 🙏 Agradecimientos

- [n8n](https://n8n.io) - Plataforma de automatización
- [Anthropic](https://anthropic.com) - Claude AI
- [Google Cloud](https://cloud.google.com) - APIs de Google Workspace
- [Meta](https://business.whatsapp.com) - WhatsApp Business API

---

**¡Hecho con ❤️ para automatizar el análisis de nichos!**
