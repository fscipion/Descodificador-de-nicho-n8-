# Plantilla Email - Envío del Análisis

## Configuración en n8n

Esta plantilla está configurada directamente en el nodo de Gmail del workflow, pero aquí está la versión completa para referencia y personalización.

---

## Email Template

### Asunto
```
Tu Análisis Personalizado de Nicho: {{nicho}}
```

### Cuerpo del Email (HTML)

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333333;
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
        }
        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px;
            border-radius: 10px 10px 0 0;
            text-align: center;
        }
        .header h1 {
            margin: 0;
            font-size: 24px;
        }
        .content {
            background: #ffffff;
            padding: 30px;
            border: 1px solid #e0e0e0;
            border-top: none;
        }
        .greeting {
            font-size: 18px;
            color: #2c3e50;
            margin-bottom: 20px;
        }
        .checklist {
            background: #f8f9fa;
            padding: 20px;
            border-left: 4px solid #667eea;
            margin: 20px 0;
        }
        .checklist-item {
            padding: 8px 0;
            display: flex;
            align-items: center;
        }
        .checkmark {
            color: #28a745;
            font-size: 20px;
            margin-right: 10px;
        }
        .cta-box {
            background: #667eea;
            color: white;
            padding: 20px;
            border-radius: 8px;
            margin: 25px 0;
            text-align: center;
        }
        .cta-box p {
            margin: 10px 0;
            font-size: 16px;
        }
        .highlight {
            background: #fff3cd;
            padding: 15px;
            border-radius: 5px;
            border-left: 4px solid #ffc107;
            margin: 20px 0;
        }
        .footer {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 0 0 10px 10px;
            text-align: center;
            font-size: 14px;
            color: #666;
        }
        .button {
            display: inline-block;
            padding: 12px 30px;
            background: white;
            color: #667eea;
            text-decoration: none;
            border-radius: 5px;
            font-weight: bold;
            margin-top: 10px;
        }
        .emoji {
            font-size: 24px;
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>🚀 Tu Análisis Personalizado Está Listo</h1>
    </div>

    <div class="content">
        <p class="greeting">Hola <strong>{{nombre}}</strong>,</p>

        <p>¡Gracias por completar nuestro formulario de análisis de nicho!</p>

        <p>Hemos preparado un <strong>documento personalizado exclusivamente para {{empresa}}</strong>, enfocado en tu nicho de <strong>{{nicho}}</strong>.</p>

        <div class="checklist">
            <div class="checklist-item">
                <span class="checkmark">✅</span>
                <span><strong>Custom Instructions</strong> específicas para tu nicho</span>
            </div>
            <div class="checklist-item">
                <span class="checkmark">✅</span>
                <span><strong>Training Data</strong> con casos de éxito relevantes</span>
            </div>
            <div class="checklist-item">
                <span class="checkmark">✅</span>
                <span><strong>Plan de Acción</strong> de 30 días paso a paso</span>
            </div>
        </div>

        <p>Encontrarás el análisis completo en el <strong>documento PDF adjunto</strong> a este email.</p>

        <div class="highlight">
            <p><strong>💡 Tip:</strong> Dedica al menos 15-20 minutos a leer el documento completo. Hemos personalizado cada sección pensando específicamente en las necesidades de {{empresa}}.</p>
        </div>

        <div class="cta-box">
            <p class="emoji">📱</p>
            <p><strong>¡Queremos conocer tu opinión!</strong></p>
            <p>En las próximas <strong>24 horas</strong> te contactaremos vía WhatsApp para:</p>
            <p>• Conocer tu feedback sobre el análisis<br>
            • Resolver cualquier duda que tengas<br>
            • Ayudarte a implementar el plan de acción</p>
        </div>

        <p>Mientras tanto, si tienes alguna pregunta urgente, no dudes en responder a este email.</p>

        <p style="margin-top: 30px;">¡Estamos emocionados de ayudarte a descifrar tu nicho y hacer crecer tu negocio! 🎯</p>

        <p style="margin-top: 30px;">
            Saludos,<br>
            <strong>El equipo de Descodificador de Nicho</strong>
        </p>
    </div>

    <div class="footer">
        <p>Has recibido este email porque completaste el formulario de análisis de nicho.</p>
        <p>© 2024 Descodificador de Nicho - Todos los derechos reservados</p>
    </div>
</body>
</html>
```

---

## Versión Plain Text (Fallback)

```
Hola {{nombre}},

¡Gracias por completar nuestro formulario de análisis de nicho!

Hemos preparado un documento personalizado exclusivamente para {{empresa}}, enfocado en tu nicho de {{nicho}}.

INCLUYE:
✅ Custom Instructions específicas para tu nicho
✅ Training Data con casos de éxito relevantes
✅ Plan de Acción de 30 días paso a paso

Encontrarás el análisis completo en el documento PDF adjunto a este email.

TIP: Dedica al menos 15-20 minutos a leer el documento completo. Hemos personalizado cada sección pensando específicamente en las necesidades de {{empresa}}.

¡QUEREMOS CONOCER TU OPINIÓN! 📱

En las próximas 24 horas te contactaremos vía WhatsApp para:
• Conocer tu feedback sobre el análisis
• Resolver cualquier duda que tengas
• Ayudarte a implementar el plan de acción

Mientras tanto, si tienes alguna pregunta urgente, no dudes en responder a este email.

¡Estamos emocionados de ayudarte a descifrar tu nicho y hacer crecer tu negocio! 🎯

Saludos,
El equipo de Descodificador de Nicho

---
Has recibido este email porque completaste el formulario de análisis de nicho.
© 2024 Descodificador de Nicho - Todos los derechos reservados
```

---

## Configuración en n8n

### Variables Disponibles

El email tiene acceso a todas las variables del formulario:

- `{{nombre}}` - Nombre del cliente
- `{{empresa}}` - Nombre de la empresa
- `{{nicho}}` - Nicho de mercado
- `{{email}}` - Email del destinatario
- `{{telefono}}` - Teléfono WhatsApp
- Más cualquier campo adicional del formulario

### Configuración del Nodo Gmail

```json
{
  "sendTo": "={{$json.email}}",
  "subject": "=Tu Análisis Personalizado de Nicho: {{$json.nicho}}",
  "message": "HTML template above",
  "options": {
    "attachments": "data:application/pdf;base64,={{$json.data}}",
    "attachmentsPropertyName": "=Análisis_{{$json.empresa}}.pdf",
    "ccList": "",
    "bccList": "",
    "replyTo": "contact@descodificadordenicho.com"
  }
}
```

### Testing

Antes de activar el workflow en producción:

1. Envía un email de prueba a ti mismo
2. Verifica que:
   - Todas las variables se reemplazan correctamente
   - El PDF se adjunta correctamente
   - El formato HTML se ve bien en diferentes clientes de email
   - La versión plain text funciona como fallback

### Personalización

Puedes personalizar:

1. **Colores**: Cambia `#667eea` y `#764ba2` por los de tu marca
2. **Logo**: Añade tu logo en el header
3. **Footer**: Añade links a redes sociales
4. **Call-to-action**: Modifica el mensaje del CTA
5. **Tono**: Ajusta el tono según tu audiencia

### Optimización

- **Subject line**: Personalizado con el nicho para mayor relevancia
- **Preheader**: Primera línea del email debe ser atractiva
- **Mobile-friendly**: Responsive design que se ve bien en móviles
- **Plain text**: Incluye versión plain text para mejor deliverability

### Deliverability Tips

1. **SPF/DKIM**: Configura correctamente en tu dominio
2. **Warming**: Si es una cuenta nueva de Gmail, empieza con poco volumen
3. **Bounce rate**: Valida emails antes de enviar
4. **Spam words**: Evita palabras como "gratis", "urgente", exceso de signos
5. **Ratio texto/imagen**: Mantén un buen balance

---

## Analytics (Opcional)

Si quieres trackear opens/clicks, puedes añadir:

### Pixel de tracking
```html
<img src="https://tu-dominio.com/track/{{$json.email}}" width="1" height="1" />
```

### Links con UTM
```
?utm_source=email&utm_medium=automation&utm_campaign=analisis_nicho
```

---

## Compliance

Asegúrate de cumplir con:

- **GDPR**: Si envías a Europa
- **CAN-SPAM**: Si envías a EEUU
- **Consentimiento**: Los usuarios completaron el formulario voluntariamente

El footer incluye:
- Razón de recepción del email
- Información de la empresa
