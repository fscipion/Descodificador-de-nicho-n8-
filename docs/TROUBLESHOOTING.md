# 🔧 Guía de Solución de Problemas

Esta guía cubre los problemas más comunes y cómo solucionarlos.

---

## 📑 Tabla de Contenidos

1. [Workflow No Se Activa](#workflow-no-se-activa)
2. [Google Forms](#google-forms)
3. [Google Sheets](#google-sheets)
4. [Claude AI](#claude-ai)
5. [Google Docs](#google-docs)
6. [Gmail](#gmail)
7. [WhatsApp](#whatsapp)
8. [Errores Comunes](#errores-comunes)

---

## Workflow No Se Activa

### Síntoma
El workflow está en estado "Inactive" o no responde a eventos.

### Soluciones

#### 1. Verificar Estado del Workflow
```
- Ve a Workflows en n8n
- Verifica que el toggle "Active" está ON (verde)
- Si está OFF, actívalo
```

#### 2. Verificar Credenciales
```
- Todas las credenciales deben tener un ✅ verde
- Si alguna está en rojo, reconfigúrala
- Prueba cada credencial individualmente
```

#### 3. Verificar Variables de Entorno
```
- Settings > Variables
- Asegúrate de que todas las variables estén configuradas
- Sin espacios extra al inicio/final
```

#### 4. Revisar Logs
```
- Executions > Show recent
- Busca errores en rojo
- Lee el mensaje de error específico
```

---

## Google Forms

### Problema 1: El Trigger No Detecta Nuevas Entradas

#### Causa Común
El webhook de Google Forms no está configurado correctamente.

#### Solución
```
1. En el nodo "Google Forms Trigger":
   - Click en "Listen for Test Event"
   - Deja n8n esperando

2. Completa el formulario en Google Forms

3. Si no funciona:
   - Verifica que el Form ID sea correcto
   - Asegúrate de que la credencial de Google tiene permisos
   - Prueba desconectar y reconectar la credencial
```

#### Alternativa: Usar Google Sheets Trigger
```
Si el Google Forms Trigger no funciona:
1. Conecta tu Form a un Google Sheet (Responses > Link to Sheets)
2. Usa "Google Sheets Trigger" en vez de "Google Forms Trigger"
3. Configura para escuchar nuevas filas
```

### Problema 2: Campos del Formulario No Coinciden

#### Síntoma
Los datos no llegan correctamente al workflow.

#### Solución
```
1. Verifica que los nombres de campo en el Form coincidan exactamente:
   - email
   - nombre
   - empresa
   - nicho
   - problema
   - objetivos
   - audiencia
   - competencia
   - telefono

2. Los nombres son case-sensitive (mayúsculas/minúsculas importan)

3. En el workflow, ajusta las referencias:
   {{$json.campo_correcto}}
```

---

## Google Sheets

### Problema 1: No Se Crea Fila en el Sheet

#### Causa 1: Sheet ID Incorrecto
```
Solución:
1. Abre tu Google Sheet
2. URL: docs.google.com/spreadsheets/d/SHEET_ID/edit
3. Copia el SHEET_ID exactamente
4. Actualiza la variable GOOGLE_SHEET_TRACKING_ID
```

#### Causa 2: Nombre de Pestaña Incorrecto
```
Solución:
1. La pestaña debe llamarse exactamente "Seguimiento"
2. Sin espacios extra
3. Respeta mayúsculas/minúsculas
```

#### Causa 3: Permisos Insuficientes
```
Solución:
1. Abre el Google Sheet
2. Share > Anyone with the link can edit
3. O da permisos específicos a la cuenta de servicio de Google
```

### Problema 2: Datos Se Escriben en Columnas Incorrectas

#### Solución
```
Verifica que los headers en fila 1 coincidan exactamente:

A: timestamp
B: email
C: nombre
D: empresa
E: nicho
F: problema
G: estado
H: documento_enviado
I: whatsapp_activado
J: feedback_nota
K: notas

Si los cambiaste, actualiza el nodo de Google Sheets en n8n.
```

### Problema 3: Error "Unable to Update Row"

#### Solución
```
1. El workflow intenta actualizar una fila que no existe
2. Asegúrate de que el "match column" existe:
   - matchColumn: "email"
   - matchValue: "={{$json.email}}"
3. Verifica que el email del formulario coincide con el del Sheet
```

---

## Claude AI

### Problema 1: "API Key Invalid"

#### Solución
```
1. Ve a console.anthropic.com/settings/keys
2. Genera una nueva API key
3. Actualiza ANTHROPIC_API_KEY en n8n
4. Asegúrate de copiar la key completa (empieza con sk-ant-api03-)
```

### Problema 2: "Insufficient Credits"

#### Solución
```
1. Ve a console.anthropic.com/billing
2. Añade créditos ($10+ recomendado)
3. Espera 1-2 minutos a que se procese
4. Reintenta el workflow
```

### Problema 3: Claude No Genera 3 Outputs

#### Causa: Prompt Modificado Incorrectamente

#### Solución
```
1. Verifica que el prompt incluye:
   "Por favor, genera EXACTAMENTE 3 outputs separados por '###OUTPUT_SEPARATOR###'"

2. Verifica que el nodo "Separar Outputs de Claude" usa:
   fullResponse.split('###OUTPUT_SEPARATOR###')

3. Prueba el prompt manualmente en console.anthropic.com
```

### Problema 4: "Rate Limit Exceeded"

#### Solución
```
1. Antropic tiene límite de 50 requests/min
2. Si procesas muchos formularios:
   - Añade un nodo "Wait" de 2 segundos antes de Claude
   - O procesa en batches

3. Para límites mayores:
   - Contacta a Anthropic para upgrade
```

### Problema 5: Respuesta de Claude Es Muy Corta

#### Solución
```
1. En el nodo de Claude, verifica:
   - max_tokens: 4000 (aumenta si necesitas más)
   - temperature: 0.7 (ajusta según necesites)

2. Modifica el prompt para ser más específico:
   "Cada output debe tener entre 600-1000 palabras"
```

---

## Google Docs

### Problema 1: No Se Crea Copia del Template

#### Solución
```
1. Verifica el Template ID:
   - URL: docs.google.com/document/d/TEMPLATE_ID/edit
   - Copia el ID exactamente

2. Verifica permisos:
   - Share > Anyone with the link can view
   - O da permisos a la cuenta de servicio

3. Prueba abrir el template manualmente con el ID
```

### Problema 2: Los Placeholders No Se Reemplazan

#### Causa: Formato Incorrecto de Placeholders

#### Solución
```
Los placeholders deben ser EXACTAMENTE:
{{NOMBRE_CLIENTE}}
{{EMPRESA}}
{{NICHO}}
{{FECHA}}
{{CUSTOM_INSTRUCTIONS}}
{{TRAINING_DATA}}
{{PLAN_ACCION}}

Verifica:
1. Sin espacios: {{VARIABLE}} ✅  {{ VARIABLE }} ❌
2. Mayúsculas: {{NICHO}} ✅  {{nicho}} ❌
3. Sin caracteres especiales escondidos
```

### Problema 3: El Formato del Documento Se Rompe

#### Solución
```
1. Claude puede generar markdown que rompe el formato

2. En el nodo "Separar Outputs de Claude", añade limpieza:
   ```javascript
   const cleanOutput = (text) => {
     return text
       .replace(/```/g, '')  // Elimina code blocks
       .replace(/#{1,6}\s/g, '')  // Elimina markdown headers
       .trim();
   };
   ```

3. O usa Google Docs con formato "Plain text"
```

---

## Gmail

### Problema 1: Email No Se Envía

#### Causa 1: Credenciales Incorrectas

#### Solución
```
1. En n8n, ve a Credentials > Gmail OAuth2
2. Click en "Reconnect"
3. Autoriza todos los scopes solicitados
4. Asegúrate de aceptar el acceso a Gmail
```

#### Causa 2: Límites de Gmail

#### Solución
```
Gmail tiene límites:
- Gmail personal: 500 emails/día
- Google Workspace: 2000 emails/día

Si los excedes:
1. Espera 24 horas
2. O upgrade a Google Workspace
3. O usa un servicio SMTP alternativo
```

### Problema 2: Email Llega a Spam

#### Soluciones
```
1. Configura SPF/DKIM en tu dominio
2. Evita palabras spam: "GRATIS", "URGENTE", "!!!"
3. Incluye versión plain text además de HTML
4. No uses demasiadas imágenes
5. Warm up: empieza con poco volumen
6. Pide a los usuarios que añadan tu email a contactos
```

### Problema 3: PDF No Se Adjunta

#### Solución
```
1. Verifica que el nodo de Google Drive genera el PDF correctamente

2. En el nodo de Gmail, verifica:
   options.attachments: "data:application/pdf;base64,={{$json.data}}"

3. El $json.data debe contener el PDF en base64

4. Si falla, prueba:
   - Descargar el PDF localmente primero
   - Verificar el tamaño del PDF (<25MB)
```

---

## WhatsApp

### Problema 1: "Template Not Found"

#### Solución
```
1. Verifica que el template está APPROVED en Meta Business Suite
2. El nombre debe ser exactamente:
   - En Meta: seguimiento_analisis_24h
   - En n8n: seguimiento_analisis_24h
3. Respeta guiones bajos y minúsculas
```

### Problema 2: "Recipient Phone Number Invalid"

#### Solución
```
El formato debe ser:
+[código_país][número]

Ejemplos:
✅ +34612345678 (España)
✅ +5491123456789 (Argentina)
❌ 612345678 (falta código país)
❌ 0034612345678 (formato incorrecto)

En Google Forms, valida con regex:
^\+[1-9]\d{1,14}$
```

### Problema 3: "Message Not Delivered"

#### Causa 1: Usuario No Tiene WhatsApp

#### Solución
```
1. Verifica que el número tiene WhatsApp instalado
2. No hay forma de validar esto antes de enviar
3. Meta te dará error "not registered"
4. Registra estos casos en tu Google Sheet
```

#### Causa 2: Usuario Te Bloqueó

#### Solución
```
1. Si un usuario te bloquea, no puedes enviarle mensajes
2. Meta devuelve error "blocked"
3. Respeta esto y no reintentes
4. Elimina el número de tu lista
```

#### Causa 3: Límites Excedidos

#### Solución
```
WhatsApp tiene tiers:
- Tier 1: 1,000 conversaciones/día
- Tier 2: 10,000 conversaciones/día
- Tier 3: 100,000 conversaciones/día

Para upgrade:
1. Mantén quality rating alto
2. Envía mensajes de calidad
3. Meta te upgradeará automáticamente
4. O solicita upgrade manual
```

### Problema 4: No Recibes Respuestas del Usuario

#### Solución
```
1. Verifica webhook en Meta Business Suite:
   - URL correcta
   - Verify token correcto
   - Suscrito a "messages"

2. En n8n, verifica que el nodo "WhatsApp Trigger" está activo

3. Prueba enviando un mensaje manual a tu número de WhatsApp Business

4. Revisa logs en Meta Business Suite > Webhooks > Events
```

### Problema 5: "Quality Rating Too Low"

#### Causa
Muchos usuarios bloquean, reportan o no responden.

#### Solución
```
1. Mejora la calidad de tus mensajes:
   - Más personalizados
   - Contenido valioso
   - Buen timing

2. Solo envía a usuarios que dieron consentimiento explícito

3. Permite opt-out fácilmente

4. No hagas spam

5. Si el rating sigue bajo:
   - Meta limitará tus envíos
   - Pausa la campaña
   - Revisa tu estrategia
```

---

## Errores Comunes

### Error 1: "Variable Not Defined"

```
Error: Variable 'GOOGLE_FORM_ID' is not defined

Solución:
1. Ve a Settings > Variables en n8n
2. Añade la variable faltante
3. Formato correcto: GOOGLE_FORM_ID (sin $ ni {})
4. En el workflow usa: {{$env.GOOGLE_FORM_ID}}
```

### Error 2: "Cannot Read Property of Undefined"

```
Error: Cannot read property 'nombre' of undefined

Causa:
El objeto $json no contiene el campo esperado.

Solución:
1. Ejecuta el workflow paso a paso
2. Click en cada nodo para ver el output
3. Verifica que el campo existe en el JSON
4. Ajusta la referencia:
   {{$json.nombre}} o {{$node["Google Forms Trigger"].json.nombre}}
```

### Error 3: "Authentication Failed"

```
Solución:
1. La credencial expiró o se revocó
2. Ve a Credentials en n8n
3. Click en la credencial afectada
4. Click "Reconnect" o "Test"
5. Autoriza de nuevo
```

### Error 4: "Execution Timeout"

```
Error: Execution timed out after 120 seconds

Causa:
Un nodo tarda demasiado (usualmente Claude o Google Drive).

Solución:
1. En n8n Cloud: no se puede cambiar timeout
2. En self-hosted: aumenta EXECUTIONS_TIMEOUT en .env
3. Optimiza el workflow:
   - Reduce max_tokens de Claude
   - Simplifica el prompt
   - Reduce el tamaño del template
```

### Error 5: "Memory Limit Exceeded"

```
Causa:
El PDF o los datos son muy grandes.

Solución:
1. Reduce el tamaño del Google Doc template
2. Optimiza imágenes en el template
3. Reduce max_tokens de Claude
4. En self-hosted: aumenta memoria de Docker
```

---

## Debugging Avanzado

### 1. Modo Debug en n8n

```
1. Activa "Save execution data"
2. En cada nodo, click para ver:
   - Input data
   - Output data
   - Execution time
3. Identifica dónde falla exactamente
```

### 2. Testing Individual de Nodos

```
1. Desactiva el workflow completo
2. Crea un workflow de prueba
3. Copia un nodo problemático
4. Usa "Execute Node" con datos de prueba
5. Itera hasta que funcione
```

### 3. Logs de APIs Externas

#### Google
```
- Ve a console.cloud.google.com
- Logging > Logs Explorer
- Filtra por tu proyecto
- Busca errores
```

#### Anthropic
```
- console.anthropic.com no tiene logs detallados
- Usa los logs de n8n
```

#### WhatsApp
```
- business.facebook.com
- WhatsApp > Insights
- Revisa mensajes fallidos
```

### 4. Monitoreo en Tiempo Real

```
1. En n8n, ve a Executions
2. Activa "Auto refresh"
3. Completa un formulario de prueba
4. Observa la ejecución en tiempo real
5. Click en cada nodo para ver el estado
```

---

## Prevención de Problemas

### Checklist Pre-Producción

- [ ] Test end-to-end completado
- [ ] Todas las credenciales verificadas
- [ ] Variables de entorno configuradas
- [ ] Templates de WhatsApp APPROVED
- [ ] Límites de APIs verificados
- [ ] Backup del Google Sheet configurado
- [ ] Notificaciones de error activadas
- [ ] Documentación actualizada

### Monitoreo Continuo

```
1. Diario:
   - Revisa ejecuciones fallidas
   - Verifica que no hay errores acumulados

2. Semanal:
   - Revisa créditos de APIs
   - Analiza feedback de usuarios
   - Optimiza basándote en datos

3. Mensual:
   - Audita permisos de Google
   - Rota API keys
   - Revisa compliance
   - Actualiza documentación
```

---

## Obtener Ayuda

### Recursos Oficiales

- **n8n**: [community.n8n.io](https://community.n8n.io)
- **Anthropic**: [discord.gg/anthropic](https://discord.gg/anthropic)
- **WhatsApp**: [developers.facebook.com/support](https://developers.facebook.com/support)
- **Google**: [support.google.com/cloud](https://support.google.com/cloud)

### Información a Incluir Cuando Pidas Ayuda

```
1. Descripción del problema
2. Mensaje de error exacto
3. Paso donde falla en el workflow
4. Qué has intentado
5. Screenshots relevantes
6. Logs (sin credenciales sensibles)
7. Versiones:
   - n8n
   - Nodos específicos
```

---

**¿Sigue sin funcionar? Abre un issue en GitHub con los detalles.**
