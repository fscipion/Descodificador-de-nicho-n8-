# Plantilla WhatsApp - Seguimiento 24h

## Configuración en Meta Business Suite

Para usar WhatsApp Business API, necesitas crear templates aprobados por Meta. Aquí está la estructura completa.

---

## Template Principal: Seguimiento 24h

### Información Básica

- **Nombre del template**: `seguimiento_analisis_24h`
- **Categoría**: UTILITY (recomendado) o MARKETING
- **Idioma**: Spanish (es)
- **Status**: Debe estar APPROVED antes de usar

### Contenido del Template

#### HEADER (Opcional pero recomendado)
```
EMOJI: 👋
```

#### BODY
```
Hola {{1}},

Hace 24 horas te enviamos tu análisis personalizado de nicho para {{2}}.

¿Ya tuviste oportunidad de revisarlo?

Nos encantaría conocer tu opinión y ayudarte con cualquier duda que tengas sobre el documento.

¿Tienes unos minutos para conversar?
```

#### FOOTER (Opcional)
```
Descodificador de Nicho
```

#### BUTTONS (Opcionales)
- Button 1: Quick Reply - "Sí, lo revisé"
- Button 2: Quick Reply - "Aún no lo vi"
- Button 3: Quick Reply - "Tengo dudas"

### Variables

- `{{1}}` = Nombre del cliente (ej: "Carlos")
- `{{2}}` = Nombre de la empresa (ej: "Marketing Pro")

---

## Templates Adicionales

### Template 2: Solicitud de Feedback

**Nombre**: `solicitar_feedback_nota`
**Categoría**: UTILITY
**Idioma**: Spanish

**Body**:
```
¡Gracias por tu respuesta! 🙌

Nos encantaría conocer tu opinión sobre el análisis de nicho que te enviamos.

¿Qué nota le darías del 0 al 10?

Simplemente responde con un número.
```

**Nota**: Este template NO requiere variables.

---

### Template 3: Agradecimiento por Feedback

**Nombre**: `agradecimiento_feedback`
**Categoría**: UTILITY
**Idioma**: Spanish

**Body**:
```
¡Muchas gracias por tu valoración de {{1}}/10! 🎯

Nos ayuda mucho a mejorar.

¿Hay algo específico que te gustaría comentar sobre el análisis?

Estamos aquí para ayudarte en lo que necesites.
```

**Variables**:
- `{{1}}` = Nota recibida (ej: "9")

---

## Configuración en n8n

### Nodo 1: WhatsApp - Enviar Mensaje 24h

```json
{
  "operation": "sendTemplate",
  "phoneNumberId": "={{$env.WHATSAPP_PHONE_NUMBER_ID}}",
  "recipientPhoneNumber": "={{$json.telefono}}",
  "template": "seguimiento_analisis_24h",
  "templateLanguage": "es",
  "components": {
    "values": [
      {
        "type": "body",
        "parameters": [
          {
            "type": "text",
            "text": "={{$json.nombre}}"
          },
          {
            "type": "text",
            "text": "={{$json.empresa}}"
          }
        ]
      }
    ]
  }
}
```

### Nodo 2: WhatsApp - Preguntar Feedback

Este mensaje se envía DESPUÉS de que el usuario responda, por lo que NO necesita template aprobado (ventana de 24h activa).

```json
{
  "operation": "send",
  "phoneNumberId": "={{$env.WHATSAPP_PHONE_NUMBER_ID}}",
  "recipientPhoneNumber": "={{$json.from}}",
  "message": "¡Gracias por tu respuesta! 🙌\n\nNos encantaría conocer tu opinión sobre el análisis de nicho que te enviamos.\n\n¿Qué nota le darías del 0 al 10?\n\nSimplemente responde con un número."
}
```

### Nodo 3: WhatsApp - Agradecer Feedback

También dentro de la ventana de 24h (mensaje libre):

```json
{
  "operation": "send",
  "phoneNumberId": "={{$env.WHATSAPP_PHONE_NUMBER_ID}}",
  "recipientPhoneNumber": "={{$json.from}}",
  "message": "=¡Muchas gracias por tu valoración de {{$json.message.text}}/10! 🎯\n\nNos ayuda mucho a mejorar. ¿Hay algo específico que te gustaría comentar sobre el análisis?\n\nEstamos aquí para ayudarte en lo que necesites."
}
```

---

## Formato de Número de Teléfono

### Formato Requerido
```
+[código_país][número]
```

### Ejemplos Válidos
- España: `+34612345678`
- México: `+521234567890`
- Argentina: `+5491123456789`
- Colombia: `+573001234567`
- Chile: `+56912345678`

### Validación en Google Form
```regex
^\+[1-9]\d{1,14}$
```

---

## Proceso de Aprobación de Templates

### Paso 1: Crear el Template

1. Ve a [Meta Business Suite](https://business.facebook.com/)
2. Selecciona tu cuenta de WhatsApp Business
3. Ve a **Message Templates**
4. Click en **Create Template**

### Paso 2: Llenar la Información

- **Template name**: Sin espacios, snake_case
- **Category**: UTILITY (más rápida aprobación) o MARKETING
- **Languages**: Spanish

### Paso 3: Diseñar el Mensaje

- **Header**: Opcional, puede ser texto, imagen o emoji
- **Body**: El mensaje principal (máx 1024 caracteres)
- **Footer**: Opcional, info de tu empresa
- **Buttons**: Opcional, hasta 3 botones

### Paso 4: Enviar a Revisión

- Click en **Submit**
- Meta revisará en 24-48 horas (usualmente menos)
- Recibirás notificación del estado

### Paso 5: Usar en n8n

Una vez APPROVED:
- Copia el nombre exacto del template
- Úsalo en el nodo de WhatsApp en n8n

---

## Límites y Restricciones

### WhatsApp Business API

1. **Ventana de 24 horas**:
   - Después de que un usuario te escriba, tienes 24h para enviar mensajes libres
   - Fuera de esa ventana, SOLO puedes enviar templates aprobados

2. **Templates**:
   - Deben ser aprobados por Meta antes de usar
   - No pueden ser muy promocionales
   - Deben aportar valor al usuario

3. **Rate Limits**:
   - Tier 1: 1,000 conversaciones/día
   - Tier 2: 10,000 conversaciones/día
   - Tier 3: 100,000 conversaciones/día

4. **Quality Rating**:
   - Si muchos usuarios bloquean o reportan, tu rating baja
   - Rating bajo = menos mensajes permitidos

### Mejores Prácticas

✅ **SÍ hacer**:
- Obtener consentimiento explícito (como el formulario)
- Enviar contenido relevante y personalizado
- Respetar horarios razonables
- Facilitar opt-out
- Responder rápido a mensajes del usuario

❌ **NO hacer**:
- Spam o mensajes masivos no solicitados
- Contenido engañoso
- Información sensible sin cifrar
- Enviar fuera de horarios razonables

---

## Testing

### Antes de Producción

1. **Números de prueba**: Usa el número de prueba de Meta
2. **Template test**: Envía templates a ti mismo primero
3. **Variables**: Verifica que se reemplazan correctamente
4. **Webhooks**: Asegúrate de recibir las respuestas
5. **Fallbacks**: Ten plan B si el mensaje falla

### Números de Prueba

En Meta Business Suite puedes añadir hasta 5 números de prueba para testing gratuito.

---

## Webhook Configuration

Para recibir respuestas de WhatsApp en n8n:

### En Meta Business Suite

1. Ve a **WhatsApp** > **Configuration**
2. En **Webhooks**, añade:
   - **Callback URL**: URL del webhook de n8n
   - **Verify Token**: Token secreto que elijas

### En n8n

El nodo **WhatsApp Trigger** automáticamente:
- Genera una URL de webhook
- Espera las respuestas de los usuarios
- Parsea el contenido del mensaje

---

## Variables Disponibles

### Del Formulario (via workflow)
- `{{nombre}}` - Nombre del cliente
- `{{empresa}}` - Empresa
- `{{nicho}}` - Nicho
- `{{email}}` - Email
- `{{telefono}}` - Teléfono WhatsApp

### De Respuestas WhatsApp
- `{{from}}` - Número que envió el mensaje
- `{{message.text}}` - Contenido del mensaje
- `{{message.timestamp}}` - Momento del mensaje
- `{{message.id}}` - ID único del mensaje

---

## Analytics y Métricas

### Métricas a Trackear

1. **Delivery Rate**: % de mensajes entregados
2. **Read Rate**: % de mensajes leídos
3. **Response Rate**: % de usuarios que responden
4. **Feedback Rate**: % que dan nota de feedback
5. **Average Rating**: Nota promedio recibida

### Implementación

Usa los nodos de Google Sheets en n8n para registrar:
- Timestamp de cada mensaje
- Estado (entregado, leído, respondido)
- Contenido de respuesta
- Nota de feedback

---

## Troubleshooting

### El mensaje no se envía

1. Verifica que el template esté APPROVED
2. Comprueba el Phone Number ID
3. Valida el formato del número de teléfono
4. Revisa los créditos de tu cuenta WhatsApp Business

### El usuario no recibe el mensaje

1. Número de teléfono válido y activo
2. Usuario no te ha bloqueado
3. Usuario tiene WhatsApp instalado
4. Estás dentro de los límites de tu tier

### No recibes las respuestas

1. Webhook configurado correctamente
2. URL pública accesible
3. Verify token correcto
4. Subscripciones de webhook activas

---

## Escalado

### Para Alto Volumen

1. **Upgrade Tier**: Solicita tier superior a Meta
2. **Rate Limiting**: Implementa delays entre mensajes
3. **Batch Processing**: Agrupa envíos en lotes
4. **Error Handling**: Retry logic para fallos
5. **Monitoring**: Alertas si delivery rate baja

---

## Compliance

### GDPR / Privacidad

- ✅ Consentimiento explícito obtenido (formulario)
- ✅ Opción de opt-out clara
- ✅ Datos encriptados en tránsito
- ✅ No compartir datos con terceros
- ✅ Permitir eliminación de datos

### WhatsApp Commerce Policy

Lee y cumple con:
- [WhatsApp Commerce Policy](https://www.whatsapp.com/legal/commerce-policy)
- [Meta Business Tools Terms](https://www.facebook.com/legal/terms/businesstools)
