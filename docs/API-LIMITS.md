# 📊 Límites de APIs y Costos

Guía completa sobre límites, rate limits, quotas y costos de todas las APIs utilizadas.

---

## 📑 Tabla de Contenidos

1. [Google Workspace](#google-workspace)
2. [Anthropic Claude](#anthropic-claude)
3. [WhatsApp Business](#whatsapp-business)
4. [n8n](#n8n)
5. [Calculadora de Costos](#calculadora-de-costos)

---

## Google Workspace

### Gmail API

#### Quotas (Gmail Personal)
| Tipo | Límite |
|------|--------|
| Emails enviados por día | 500 |
| Emails enviados por mensaje | 1 |
| Tamaño máximo del email | 25 MB |
| Adjuntos por email | 10 |
| Rate limit | 250 quota units/usuario/segundo |

#### Quotas (Google Workspace)
| Tipo | Límite |
|------|--------|
| Emails enviados por día | 2,000 |
| Emails enviados por mensaje | 1 |
| Tamaño máximo del email | 25 MB |
| Adjuntos por email | 10 |
| Rate limit | 250 quota units/usuario/segundo |

#### Costo
- **Gmail Personal**: Gratis
- **Google Workspace Business Starter**: $6/usuario/mes
- **Google Workspace Business Standard**: $12/usuario/mes

### Google Forms API

#### Quotas
| Tipo | Límite |
|------|--------|
| Respuestas de formulario | Ilimitadas |
| Tamaño máximo del formulario | 2 MB |
| Preguntas por formulario | 300 |
| Opciones por pregunta | 1,000 |
| Rate limit | 100 requests/100 segundos/usuario |

#### Costo
- **Gratis** (incluido con cuenta de Google)

### Google Sheets API

#### Quotas
| Tipo | Límite |
|------|--------|
| Read requests | 300/minuto/proyecto |
| Write requests | 300/minuto/proyecto |
| Celdas totales en Sheet | 10,000,000 |
| Filas por Sheet | 40,000 |
| Columnas por Sheet | 18,278 |
| Tamaño de celda | 50,000 caracteres |

#### Costo
- **Gratis** hasta las quotas gratuitas
- Si necesitas más: Contactar a Google Cloud

#### Optimización
```javascript
// En vez de escribir fila por fila (300 writes)
// Escribe en batch (1 write)

// ❌ Malo
for (let i = 0; i < 100; i++) {
  await sheets.append({row: data[i]});  // 100 writes
}

// ✅ Bueno
await sheets.batchUpdate({rows: data});  // 1 write
```

### Google Docs API

#### Quotas
| Tipo | Límite |
|------|--------|
| Read requests | 300/minuto/proyecto |
| Write requests | 300/minuto/proyecto |
| Tamaño máximo del documento | 50 MB |
| Tamaño máximo por request | 10 MB |

#### Costo
- **Gratis** hasta las quotas gratuitas

### Google Drive API

#### Quotas
| Tipo | Límite |
|------|--------|
| Queries per day | 1,000,000,000 |
| Queries per 100 segundos | 1,000 |
| Queries per 100 segundos/usuario | 100 |
| Tamaño de archivo | 5 TB |
| Almacenamiento (gratis) | 15 GB compartidos |

#### Costo
- **Google Drive Personal**: 15 GB gratis
  - 100 GB: $1.99/mes
  - 200 GB: $2.99/mes
  - 2 TB: $9.99/mes
- **Google Workspace**: Según el plan

#### Conversión de Formatos (Export)
| De | A | Límite |
|----|---|--------|
| Google Docs | PDF | 10 MB por request |
| Google Docs | DOCX | 10 MB por request |

---

## Anthropic Claude

### Rate Limits

#### Claude 3.5 Sonnet (Recomendado)
| Métrica | Tier 1 | Tier 2 | Tier 3 | Tier 4 |
|---------|--------|--------|--------|--------|
| Requests/min | 50 | 1,000 | 2,000 | 4,000 |
| Tokens/min | 40,000 | 80,000 | 400,000 | 800,000 |
| Tokens/day | 1,000,000 | 2,000,000 | 10,000,000 | 20,000,000 |

**Notas**:
- Tier 1: Por defecto al crear cuenta
- Tier 2+: Automático después de usar créditos y mantener buen historial
- Los límites son por organización, no por API key

### Precios

#### Modelos Disponibles
| Modelo | Input ($/MTok) | Output ($/MTok) | Mejor Para |
|--------|---------------|----------------|-----------|
| Claude 3.5 Sonnet | $3.00 | $15.00 | **Balance ideal** (recomendado) |
| Claude 3 Opus | $15.00 | $75.00 | Máxima calidad |
| Claude 3 Haiku | $0.25 | $1.25 | Velocidad y bajo costo |

**MTok** = Millón de tokens (~750,000 palabras)

### Cálculo de Costos por Análisis

Para nuestro workflow con **Claude 3.5 Sonnet**:

```
Input Tokens:
- Prompt base: ~800 tokens
- Datos del formulario: ~300 tokens
- Total input: ~1,100 tokens

Output Tokens:
- Custom Instructions: ~800 palabras = ~1,000 tokens
- Training Data: ~1,000 palabras = ~1,250 tokens
- Plan de Acción: ~800 palabras = ~1,000 tokens
- Total output: ~3,250 tokens

Costo por análisis:
Input:  1,100 tokens × $3.00/MTok = $0.0033
Output: 3,250 tokens × $15.00/MTok = $0.0487
TOTAL: ~$0.052 por análisis

Con $10 USD:
$10 / $0.052 = ~192 análisis
```

### Optimización de Costos

#### 1. Usar Haiku para Tareas Simples
```javascript
// Para validaciones o resúmenes cortos
model: "claude-3-haiku-20240307"
// Ahorra ~10x en costos
```

#### 2. Reducir max_tokens
```javascript
// En vez de 4000
max_tokens: 3000  // Ahorra ~25%
```

#### 3. Prompt Engineering
```javascript
// Instrucciones claras = menos tokens desperdiciados
// "Responde en 800 palabras exactas" > "Responde brevemente"
```

#### 4. Cachear Prompts (Próximamente)
```javascript
// Anthropic está desarrollando prompt caching
// Podrás reutilizar partes del prompt entre llamadas
```

### Context Window

| Modelo | Context Window |
|--------|----------------|
| Claude 3.5 Sonnet | 200,000 tokens (~150,000 palabras) |
| Claude 3 Opus | 200,000 tokens |
| Claude 3 Haiku | 200,000 tokens |

**Para nuestro caso**: Usamos ~4,350 tokens (~2% del límite), así que no hay problema.

---

## WhatsApp Business

### Tiers y Límites

WhatsApp usa un sistema de tiers que escala automáticamente:

| Tier | Conversaciones/Día | Cómo Alcanzar |
|------|-------------------|---------------|
| Tier 1 | 1,000 | Por defecto al iniciar |
| Tier 2 | 10,000 | Automático después de 7 días con buen quality rating |
| Tier 3 | 100,000 | Automático después de 7 días en Tier 2 |
| Tier 4 | Ilimitado | Solicitud manual a Meta |

### Quality Rating

Tu rating afecta cuánto puedes enviar:

| Rating | Estado | Límite |
|--------|--------|--------|
| High | 🟢 | Límite completo del tier |
| Medium | 🟡 | Límite reducido (varía) |
| Low | 🔴 | Fuertemente limitado |

**Factores que afectan el rating**:
- ✅ Usuarios responden positivamente
- ❌ Usuarios bloquean tu número
- ❌ Usuarios reportan spam
- ❌ Mensajes no entregados

### Tipos de Conversaciones

WhatsApp cobra por "conversación" de 24h:

| Tipo | Definición | Precio Base (puede variar por país) |
|------|-----------|-------------------------------------|
| Marketing | Templates promocionales | ~$0.05-0.10 por conversación |
| Utility | Templates transaccionales | ~$0.02-0.05 por conversación |
| Authentication | OTP, verificaciones | ~$0.02-0.04 por conversación |
| Service | Usuario inicia conversación | Gratis primeras 1,000/mes, luego ~$0.01 |

**Nota**: Los precios varían según el país del destinatario.

### Ventana de 24 Horas

```
Usuario escribe → Se abre ventana de 24h
Durante 24h → Puedes enviar mensajes gratis (sin templates)
Después de 24h → Solo puedes enviar templates aprobados
```

### Límites por Mensaje

| Límite | Valor |
|--------|-------|
| Longitud del mensaje | 4,096 caracteres |
| Variables en template | 4 por template |
| Botones por mensaje | 3 (templates) o 10 (dentro de ventana) |
| Tamaño de media | 16 MB (imagen), 64 MB (video) |

### Cálculo de Costos

**Escenario 1: 100 formularios/mes**
```
Envíos iniciales: 100 × $0.04 (utility) = $4.00
Respuestas (50%): 50 × $0.00 (gratis) = $0.00
TOTAL: ~$4.00/mes
```

**Escenario 2: 1,000 formularios/mes**
```
Envíos iniciales: 1,000 × $0.04 = $40.00
Respuestas (50%): 500 × $0.00 = $0.00
TOTAL: ~$40.00/mes
```

**Escenario 3: 10,000 formularios/mes**
```
Envíos iniciales: 10,000 × $0.04 = $400.00
Respuestas (50%): 5,000 × $0.00 = $0.00
TOTAL: ~$400.00/mes
```

### Optimización de Costos

#### 1. Usa Templates UTILITY (no MARKETING)
```
Utility: ~$0.02-0.05
Marketing: ~$0.05-0.10
Ahorro: ~50%
```

#### 2. Responde Dentro de 24h
```
Dentro de ventana: Gratis
Fuera de ventana: Requiere template ($$$)
```

#### 3. Reduce Mensajes de Seguimiento
```
// En vez de 3 mensajes:
Mensaje 1: Template inicial → $0.04
Mensaje 2: Recordatorio → $0.04
Mensaje 3: Último intento → $0.04
Total: $0.12

// Un solo mensaje efectivo:
Mensaje 1: Template bien diseñado → $0.04
Total: $0.04
Ahorro: 67%
```

---

## n8n

### n8n Cloud

#### Planes y Límites

| Plan | Precio | Executions/mes | Data Transfer | Workflows |
|------|--------|----------------|---------------|-----------|
| Starter | $20/mes | 2,500 | 100 GB | Unlimited |
| Pro | $50/mes | 10,000 | 500 GB | Unlimited |
| Enterprise | Custom | Custom | Custom | Unlimited |

**Notas**:
- 1 execution = 1 ejecución completa del workflow
- Data transfer = Datos procesados por n8n

### Cálculo de Executions

Para nuestro workflow:

```
1 Formulario completo = 1 execution principal + 1 sub-execution (WhatsApp response)
= 2 executions por usuario completo

Plan Starter ($20/mes):
2,500 executions / 2 = 1,250 formularios/mes

Plan Pro ($50/mes):
10,000 executions / 2 = 5,000 formularios/mes
```

### n8n Self-Hosted

#### Costos de Infraestructura

**Opción 1: VPS Básico**
```
Servidor: DigitalOcean Droplet $12/mes (2 GB RAM)
n8n: Gratis (open source)
Docker: Gratis
Total: $12/mes
Capacidad: ~500-1,000 formularios/mes
```

**Opción 2: VPS Robusto**
```
Servidor: DigitalOcean Droplet $24/mes (4 GB RAM)
n8n: Gratis
Docker: Gratis
Total: $24/mes
Capacidad: ~2,000-5,000 formularios/mes
```

**Opción 3: Empresa**
```
Servidor dedicado: $100+/mes
n8n: Gratis
Monitoreo: $20/mes
Backups: $10/mes
Total: $130+/mes
Capacidad: 10,000+ formularios/mes
```

#### Requisitos de Sistema

| Volumen | RAM | CPU | Almacenamiento |
|---------|-----|-----|----------------|
| Bajo (<100/mes) | 1 GB | 1 core | 20 GB |
| Medio (100-1,000/mes) | 2 GB | 2 cores | 40 GB |
| Alto (1,000-10,000/mes) | 4 GB | 4 cores | 100 GB |
| Muy Alto (>10,000/mes) | 8+ GB | 8+ cores | 200+ GB |

---

## Calculadora de Costos

### Calculadora Interactiva

Para **X formularios por mes**, los costos son:

#### Ejemplo: 100 Formularios/Mes

```
GOOGLE WORKSPACE:
Gmail Personal               = $0.00    (dentro de límite gratis)
Google Forms                 = $0.00    (gratis)
Google Sheets                = $0.00    (gratis)
Google Docs                  = $0.00    (gratis)
Google Drive                 = $0.00    (15GB gratis suficiente)
                              -------
Subtotal Google              = $0.00

ANTHROPIC CLAUDE:
100 análisis × $0.052        = $5.20
                              -------
Subtotal Claude              = $5.20

WHATSAPP BUSINESS:
100 envíos × $0.04           = $4.00
50 respuestas × $0.00        = $0.00    (gratis)
                              -------
Subtotal WhatsApp            = $4.00

N8N:
n8n Cloud Starter            = $20.00   (o $12 self-hosted)
                              -------
Subtotal n8n                 = $20.00

TOTAL MENSUAL                = $29.20   (Cloud) o $21.20 (Self-hosted)
Costo por formulario         = $0.29    (Cloud) o $0.21 (Self-hosted)
```

#### Ejemplo: 1,000 Formularios/Mes

```
GOOGLE WORKSPACE:
Gmail Personal               = $0.00    (dentro de límite gratis)
Google Drive (upgrade 100GB) = $1.99    (15GB no es suficiente)
Otros servicios              = $0.00    (gratis)
                              -------
Subtotal Google              = $1.99

ANTHROPIC CLAUDE:
1,000 análisis × $0.052      = $52.00
                              -------
Subtotal Claude              = $52.00

WHATSAPP BUSINESS:
1,000 envíos × $0.04         = $40.00
500 respuestas × $0.00       = $0.00
                              -------
Subtotal WhatsApp            = $40.00

N8N:
n8n Cloud Starter            = $20.00   (2,500 executions suficiente)
                              -------
Subtotal n8n                 = $20.00

TOTAL MENSUAL                = $113.99
Costo por formulario         = $0.11
```

#### Ejemplo: 10,000 Formularios/Mes

```
GOOGLE WORKSPACE:
Google Workspace Business    = $72.00   (necesario por límites de Gmail)
Google Drive en Workspace    = $0.00    (incluido)
                              -------
Subtotal Google              = $72.00

ANTHROPIC CLAUDE:
10,000 análisis × $0.052     = $520.00
                              -------
Subtotal Claude              = $520.00

WHATSAPP BUSINESS:
10,000 envíos × $0.04        = $400.00
5,000 respuestas × $0.00     = $0.00
                              -------
Subtotal WhatsApp            = $400.00

N8N:
n8n Cloud Pro                = $50.00   (10,000 executions)
                              -------
Subtotal n8n                 = $50.00

TOTAL MENSUAL                = $1,042.00
Costo por formulario         = $0.10
```

### Comparación de Planes

| Volumen | Costo Total/Mes | Costo/Formulario | Plan Recomendado |
|---------|----------------|------------------|------------------|
| 10 | $29 | $2.90 | Gmail + n8n Cloud Starter |
| 50 | $29 | $0.58 | Gmail + n8n Cloud Starter |
| 100 | $29 | $0.29 | Gmail + n8n Cloud Starter |
| 500 | $70 | $0.14 | Gmail + n8n Cloud Starter |
| 1,000 | $114 | $0.11 | Gmail + n8n Cloud Pro |
| 5,000 | $450 | $0.09 | Workspace + n8n Cloud Pro |
| 10,000 | $1,042 | $0.10 | Workspace + n8n Cloud Pro |
| 50,000+ | Custom | $0.08-0.10 | Workspace + n8n Enterprise |

### Optimización de Costos

#### Para Bajo Volumen (<100/mes)
```
✅ Gmail personal (gratis)
✅ n8n self-hosted ($12/mes VPS)
✅ Claude 3.5 Sonnet (balance)
✅ WhatsApp Utility templates
= ~$21/mes
```

#### Para Medio Volumen (100-1,000/mes)
```
✅ Gmail personal o Workspace
✅ n8n Cloud Starter
✅ Claude 3.5 Sonnet
✅ Optimizar respuestas dentro de 24h en WhatsApp
= ~$29-114/mes
```

#### Para Alto Volumen (1,000+/mes)
```
✅ Google Workspace obligatorio
✅ n8n Cloud Pro o Enterprise
✅ Claude 3.5 Sonnet (considerar Haiku para partes)
✅ WhatsApp Utility + optimizar templates
✅ Negociar con Anthropic para rate limits mayores
= Escala con volumen
```

---

## Monitoreo de Uso

### Google Cloud Console

```
1. Ve a console.cloud.google.com
2. IAM & Admin > Quotas
3. Filtra por servicio (Gmail, Drive, etc.)
4. Configura alertas al 80% del límite
```

### Anthropic Console

```
1. Ve a console.anthropic.com
2. Usage > Overview
3. Monitorea:
   - Credits remaining
   - Requests/day
   - Tokens/day
4. Configura alertas de bajo crédito
```

### Meta Business Suite

```
1. Ve a business.facebook.com
2. WhatsApp > Insights
3. Monitorea:
   - Messages sent
   - Conversations
   - Quality rating
   - Spend
```

### n8n

```
1. Settings > Usage (n8n Cloud)
2. Monitorea:
   - Executions used
   - Data transfer
   - Active workflows
```

---

## Alertas Recomendadas

```
Google APIs:
- 80% de quota diaria → Email al admin
- 90% de quota diaria → Pausar workflow

Anthropic:
- $5 restantes → Email de recarga
- $1 restante → Pausar workflow

WhatsApp:
- Quality rating baja → Revisar templates
- 80% de tier limit → Planear upgrade

n8n:
- 80% de executions → Considerar upgrade
- Workflow fails > 5% → Investigar
```

---

**Usa esta guía para planear tu presupuesto y escalar de forma sostenible.**
