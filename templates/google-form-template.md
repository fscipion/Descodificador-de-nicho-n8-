# Plantilla Google Form - Análisis de Nicho

## Configuración del Formulario

### Título
**"Análisis Personalizado de Tu Nicho - Descodificador de Nicho"**

### Descripción
```
¡Obtén un análisis completo y personalizado de tu nicho de mercado!

Completa este formulario y recibirás:
✅ Custom Instructions específicas para tu negocio
✅ Training Data con casos de éxito relevantes
✅ Plan de Acción de 30 días paso a paso

Todo generado por IA y entregado en un documento PDF profesional.

Tiempo estimado: 5-7 minutos
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

### 3. Empresa o Proyecto
- **Tipo**: Short answer
- **Nombre del campo**: `empresa`
- **Pregunta**: "¿Cuál es el nombre de tu empresa o proyecto?"
- **Requerido**: Sí

---

### 4. Teléfono (WhatsApp)
- **Tipo**: Short answer
- **Nombre del campo**: `telefono`
- **Pregunta**: "Número de WhatsApp (incluye código de país, ej: +34612345678)"
- **Requerido**: Sí
- **Validación**: Regex `^\+[1-9]\d{1,14}$`
- **Mensaje de error**: "Por favor ingresa un número válido con código de país (ej: +34612345678)"

---

### 5. Tu Nicho de Mercado
- **Tipo**: Short answer
- **Nombre del campo**: `nicho`
- **Pregunta**: "¿Cuál es tu nicho de mercado?"
- **Descripción**: "Ej: Coaching para emprendedores tech, Consultoría de marketing digital para clínicas, etc."
- **Requerido**: Sí

---

### 6. Problema Principal
- **Tipo**: Paragraph
- **Nombre del campo**: `problema`
- **Pregunta**: "¿Cuál es el problema principal que resuelves para tus clientes?"
- **Descripción**: "Sé específico. ¿Qué dolor o frustración tienen antes de trabajar contigo?"
- **Requerido**: Sí

---

### 7. Objetivos
- **Tipo**: Paragraph
- **Nombre del campo**: `objetivos`
- **Pregunta**: "¿Cuáles son tus objetivos principales en los próximos 3-6 meses?"
- **Descripción**: "Ej: Aumentar ventas, mejorar posicionamiento, lanzar nuevo producto, etc."
- **Requerido**: Sí

---

### 8. Audiencia Target
- **Tipo**: Paragraph
- **Nombre del campo**: `audiencia`
- **Pregunta**: "Describe tu cliente ideal"
- **Descripción**: "Edad, profesión, problemas que tiene, nivel de ingresos, etc."
- **Requerido**: Sí

---

### 9. Competencia
- **Tipo**: Paragraph
- **Nombre del campo**: `competencia`
- **Pregunta**: "¿Quiénes son tus principales competidores?"
- **Descripción**: "Nombres o tipos de competidores. ¿Qué hacen bien? ¿Dónde ves oportunidades?"
- **Requerido**: Sí

---

### 10. Información Adicional (Opcional)
- **Tipo**: Paragraph
- **Nombre del campo**: `info_adicional`
- **Pregunta**: "¿Hay algo más que deberíamos saber sobre tu negocio?"
- **Requerido**: No

---

## Mensaje de Confirmación

```
¡Gracias por completar el formulario!

Tu análisis personalizado está siendo generado ahora mismo.

Recibirás un email en los próximos minutos con tu documento PDF completo.

En 24 horas te contactaremos por WhatsApp para conocer tu opinión y ayudarte con cualquier duda.

¡Estamos emocionados de ayudarte a descifrar tu nicho! 🚀
```

---

## Configuración Adicional

### Settings
- **Collect email addresses**: Yes
- **Limit to 1 response**: No
- **Edit after submit**: No
- **See summary charts**: Yes

### Presentation
- **Progress bar**: Yes
- **Shuffle question order**: No
- **Show link to submit another response**: Yes

### Responses
- **Destination**: Google Sheets (crear nueva hoja o vincular a existente)
- **Get email notifications**: Yes (para el administrador)

---

## Integración con n8n

Para conectar este formulario con n8n:

1. En Google Forms, ve a **Responses**
2. Click en el icono de Google Sheets
3. Crea una nueva hoja o selecciona una existente
4. En n8n, usa el **Google Forms Trigger** con el Form ID

**Form ID** se encuentra en la URL del formulario:
```
https://docs.google.com/forms/d/FORM_ID_AQUI/edit
```

---

## Tips de Diseño

### Imagen de Header
Sube una imagen profesional relacionada con análisis de mercado o estrategia de negocio (1600 x 400 px)

### Tema
- **Color principal**: #4285F4 (azul profesional)
- **Fuente**: Modern sans-serif
- **Fondo**: Blanco limpio

### Secciones
Puedes dividir el formulario en secciones para mejor UX:

**Sección 1**: Información Personal (preguntas 1-4)
**Sección 2**: Tu Negocio (preguntas 5-7)
**Sección 3**: Tu Mercado (preguntas 8-9)
**Sección 4**: Información Adicional (pregunta 10)
