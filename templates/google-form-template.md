# Plantilla Google Form - Descodificador de Nicho™

## Configuración del Formulario

### Título
**"Descodificador de Nicho™ - Análisis Estratégico"**

### Descripción
```
¡Descubre tu posicionamiento único en el mercado!

Completa este formulario estratégico y recibirás 3 documentos personalizados:

✅ Perfil Completo de tu Cliente Ideal
✅ Tu Misión Transformacional (copy listo para usar)
✅ Tu Método Único que te diferencia

Todo generado mediante análisis de mercado con IA y entregado en PDF profesional.

Tiempo estimado: 5 minutos
```

---

## Preguntas del Formulario

### 1. Email Address
- **Tipo**: Email
- **Nombre del campo**: `email`
- **Requerido**: Sí
- **Validación**: Formato de email válido

---

### 2. Nombre Completo
- **Tipo**: Short answer
- **Nombre del campo**: `nombre`
- **Pregunta**: "¿Cuál es tu nombre completo?"
- **Requerido**: Sí

---

### 3. Teléfono (WhatsApp)
- **Tipo**: Short answer
- **Nombre del campo**: `telefono`
- **Pregunta**: "Número de WhatsApp (incluye código de país, ej: +34612345678)"
- **Descripción**: "Lo usaremos SOLO para enviarte el seguimiento en 24h y conocer tu opinión sobre el análisis"
- **Requerido**: Sí
- **Validación**: Regex `^\+[1-9]\d{1,14}$`
- **Mensaje de error**: "Por favor ingresa un número válido con código de país (ej: +34612345678)"

---

## LAS 4 PREGUNTAS ESTRATÉGICAS DEL DESCODIFICADOR DE NICHO™

### P1: ¿Cuál es tu habilidad o expertise principal que quieres enseñar en tu curso online?

- **Tipo**: Paragraph
- **Nombre del campo**: `p1_expertise`
- **Pregunta**: "P1: ¿Cuál es tu habilidad o expertise principal que quieres enseñar en tu curso online?"
- **Descripción**:
```
Sé específico. No digas solo "Marketing" o "Coaching".

Ejemplos de respuestas óptimas:
• "Nutrición hormonal para mujeres en perimenopausia"
• "Automatización de ventas con IA para consultores"
• "LinkedIn orgánico para coaches de negocios"
```
- **Requerido**: Sí
- **Validación mínima**: 20 caracteres

---

### P2: ¿Cuál es el resultado soñado que quieres que tu curso proporcione a tus clientes ideales?

- **Tipo**: Paragraph
- **Nombre del campo**: `p2_resultado`
- **Pregunta**: "P2: ¿Cuál es el resultado soñado que quieres que tu curso proporcione a tus clientes ideales?"
- **Descripción**:
```
Describe el resultado final TANGIBLE, no el proceso.

Ejemplos de respuestas óptimas:
• "Recuperar su energía natural y eliminar la dependencia del café, sintiendo vitalidad constante durante todo el día"
• "Cerrar 3-5 clientes de +5K al mes trabajando solo 20 horas semanales, con ingresos estables y predecibles"
• "Posicionarse como autoridad en su nicho y cerrar 2-3 clientes mensuales sin llamadas en frío"
```
- **Requerido**: Sí
- **Validación mínima**: 30 caracteres

---

### P3: ¿Quién necesita y experimentará el mayor impacto del resultado de tu curso online?

- **Tipo**: Paragraph
- **Nombre del campo**: `p3_target`
- **Pregunta**: "P3: ¿Quién necesita y experimentará el mayor impacto del resultado de tu curso online?"
- **Descripción**:
```
Define tu cliente ideal con MÁXIMO detalle: edad, ocupación, situación, dolor.

Ejemplos de respuestas óptimas:
• "Madres profesionales de 35-50 años con jornadas de +10 horas que sufren fatiga crónica"
• "Consultores freelance con 2-5 años de experiencia que cobran menos de 2K/mes"
• "Coaches de negocios que dependen de referidos y quieren un sistema predecible de leads"
```
- **Requerido**: Sí
- **Validación mínima**: 40 caracteres

---

### P4: ¿Cuántos clientes ya has transformado y en cuánto tiempo logran esta transformación?

- **Tipo**: Paragraph
- **Nombre del campo**: `p4_transformaciones`
- **Pregunta**: "P4: ¿Cuántos clientes ya has transformado y en cuánto tiempo logran esta transformación?"
- **Descripción**:
```
Incluye NÚMEROS y TIEMPO. Esto valida tu método.

Ejemplos de respuestas óptimas:
• "Más de 100 mujeres han recuperado su energía en 12 semanas"
• "47 consultores cerraron su primer cliente de +5K en 60 días"
• "32 coaches han generado su primer pipeline predecible en 90 días"

Si aún no tienes clientes, escribe: "Aún no tengo clientes pagando, pero tengo la metodología lista"
```
- **Requerido**: Sí
- **Validación mínima**: 20 caracteres

---

## Mensaje de Confirmación

```
¡Gracias por completar el Descodificador de Nicho™!

Tu análisis estratégico está siendo generado ahora mismo mediante IA.

Recibirás un email en los próximos minutos con tu PDF personalizado que incluye:

1️⃣ Perfil Completo de tu Cliente Ideal
   (demográficos, psicográficos, miedos, objetivos)

2️⃣ Tu Misión Transformacional
   (copy listo para usar en tu web y marketing)

3️⃣ Tu Método Único
   (diferenciador vs. competencia)

En 24 horas te contactaremos por WhatsApp para conocer tu opinión y ayudarte con cualquier duda.

¡Esperamos que revolucione tu posicionamiento! 🎯

— El equipo de Descodificador de Nicho™
```

---

## Configuración Adicional

### Settings
- **Collect email addresses**: Yes
- **Limit to 1 response**: No (permite múltiples si refinan)
- **Edit after submit**: No
- **See summary charts**: Yes (para ti)

### Presentation
- **Progress bar**: Yes
- **Shuffle question order**: No (el orden es importante)
- **Show link to submit another response**: Yes

### Responses
- **Destination**: Google Sheets (crear nueva hoja "Respuestas Descodificador")
- **Get email notifications**: Yes (para monitorear)

---

## Integración con n8n

Para conectar este formulario con n8n:

1. En Google Forms, ve a **Responses**
2. Click en el icono de Google Sheets
3. Crea una nueva hoja "Respuestas Descodificador de Nicho"
4. En n8n, usa el **Google Forms Trigger** con el Form ID

**Form ID** se encuentra en la URL del formulario:
```
https://docs.google.com/forms/d/FORM_ID_AQUI/edit
```

---

## Mapeo de Campos

Asegúrate de que el workflow de n8n mapea estos campos:

| Campo en Form | Variable en n8n |
|---------------|-----------------|
| timestamp | `$json.timestamp` |
| email | `$json.email` |
| nombre | `$json.nombre` |
| telefono | `$json.telefono` |
| p1_expertise | `$json.p1_expertise` |
| p2_resultado | `$json.p2_resultado` |
| p3_target | `$json.p3_target` |
| p4_transformaciones | `$json.p4_transformaciones` |

---

## Tips de Diseño

### Imagen de Header
Sube una imagen profesional que represente:
- Estrategia
- Análisis
- Claridad
- Posicionamiento

Dimensiones recomendadas: 1600 x 400 px

### Tema
- **Color principal**: #667eea (morado profesional) o tu color de marca
- **Fuente**: Modern sans-serif (recomendado: Inter o Roboto)
- **Fondo**: Blanco limpio

### Secciones

Divide el formulario en secciones para mejor UX:

**Sección 1**: "Información de Contacto"
(Preguntas 1-3: Email, Nombre, Teléfono)

**Sección 2**: "Las 4 Preguntas Estratégicas"
(Preguntas 4-7: P1, P2, P3, P4)

Añade una descripción introductoria en la Sección 2:
```
"Estas 4 preguntas son la base del análisis.
Tómate tu tiempo para responder con detalle.
Cuanto más específico seas, mejor será tu análisis."
```

---

## Validaciones Importantes

### Para P1 (Expertise):
```
Longitud mínima: 20 caracteres
Mensaje si es muy corto: "Por favor, sé más específico sobre tu expertise"
```

### Para P2 (Resultado):
```
Longitud mínima: 30 caracteres
Mensaje si es muy corto: "Describe el resultado tangible que obtendrán"
```

### Para P3 (Target):
```
Longitud mínima: 40 caracteres
Mensaje si es muy corto: "Define tu cliente ideal con más detalle (edad, ocupación, situación)"
```

### Para P4 (Transformaciones):
```
Longitud mínima: 20 caracteres
Mensaje si es muy corto: "Incluye números y tiempo de transformación"
```

---

## Testing

Antes de lanzar el formulario:

1. **Complétalo tú mismo** con respuestas de prueba
2. **Verifica el Google Sheet** que se crea con las respuestas
3. **Revisa los nombres de columna** (deben coincidir con el workflow)
4. **Prueba en móvil** - la mayoría lo completarán desde el teléfono
5. **Timing** - ¿realmente toma 5 minutos?

---

## Optimización de Conversión

### Landing Page
Si promocionas el form, menciona:
- ✅ "Análisis GRATIS"
- ✅ "Recibes PDF en minutos"
- ✅ "3 documentos estratégicos personalizados"
- ✅ "Sin compromiso"

### Expectativa de Tiempo
- Realista: 5-7 minutos
- NO digas "1 minuto" (no es creíble)

### Social Proof
Añade en la descripción (si tienes):
```
"Más de 500 emprendedores ya han clarificado su nicho con nuestro análisis"
```

---

## Compliance y Privacidad

Añade al final del formulario (antes de submit):

```
Al completar este formulario aceptas:
• Recibir tu análisis personalizado por email
• Recibir un mensaje de seguimiento por WhatsApp en 24h
• Que almacenemos tus respuestas para generar tu análisis

No compartimos tu información con terceros.
Puedes solicitar eliminación de tus datos en cualquier momento.
```

---

## Promoción del Formulario

### URL Acortada
Usa un servicio como Bitly para crear:
```
https://bit.ly/descodificador-nicho
```

### QR Code
Genera un QR code del formulario para:
- Presentaciones
- Material impreso
- Stories de Instagram

### Call to Action
En redes sociales:
```
"¿Confuso sobre tu nicho y posicionamiento?

Completa 4 preguntas y recibe:
✅ Perfil de tu Cliente Ideal
✅ Tu Misión Transformacional
✅ Tu Método Único

Link en bio 👆
```

---

**¡Tu formulario es la puerta de entrada a claridad estratégica! Hazlo simple y directo. 🎯**
