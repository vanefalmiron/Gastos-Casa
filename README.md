# 🧾 Gastos Casa — Automatización de Tickets con IA

Automatización construida en **Make.com** que captura tickets y facturas enviados por Telegram, los analiza con inteligencia artificial (GPT-4o-mini) y registra los datos extraídos automáticamente en Google Sheets.


 <img width="1282" height="340" alt="imagen" src="https://github.com/user-attachments/assets/2960621e-fdef-4bfc-b2b8-377220332baa" />

---

## 📋 Descripción

Este proyecto elimina la necesidad de introducir manualmente los gastos del hogar. Basta con fotografiar un ticket o factura y enviarlo por Telegram como archivo. La automatización se encarga del resto: extrae todos los datos relevantes y los guarda en una hoja de cálculo estructurada.

---

## 🔄 Flujo de la Automatización

```
📱 Telegram  →  📥 Descarga  →  🤖 OpenAI Vision  →  🔍 Parse JSON  →  📊 Google Sheets
(Envío ticket)   (archivo)      (extrae datos)        (estructura)      (guarda fila)
```

### Módulos (Make.com)

| # | Módulo | Descripción |
|---|--------|-------------|
| 1 | **Telegram Bot — Watch Updates** | Escucha mensajes entrantes en el bot |
| 21 | **Telegram Bot — Download a File** | Descarga el archivo adjunto enviado |
| 31 | **OpenAI — Analyze Images (Vision)** | Analiza la imagen y extrae los datos del ticket en formato JSON |
| 33 | **JSON — Parse JSON** | Convierte la respuesta de OpenAI en campos mapeables |
| 40 | **Google Sheets — Add a Row** | Inserta una nueva fila con los datos extraídos |

---

## 🗂️ Estructura de Datos

Los datos extraídos se guardan en Google Sheets con las siguientes columnas:

| Columna | Campo | Descripción |
|---------|-------|-------------|
| A | `fecha` | Fecha del ticket (formato `YYYY-MM-DD`) |
| B | `importe` | Total pagado (ej: `23,54`) |
| C | `iva` | Cuota de IVA (ej: `4,95`) |
| D | `categoria` | Tipo de gasto (Gasolina, Supermercado, etc.) |
| E | `empresa` | Nombre del vendedor o emisor |
| F | `cif_nif` | Identificación fiscal del emisor |
| G | `numero_factura` | Número o ID único del ticket/factura |

> Los valores numéricos usan **coma** como separador decimal (`23,54`). Si algún dato no existe en el ticket, se registra como `null`.

---

## ⚙️ Configuración y Requisitos

### Servicios necesarios

- Cuenta en **[Make.com](https://www.make.com)**
- Bot de **Telegram** (creado con [@BotFather](https://t.me/BotFather))
- API Key de **OpenAI** con acceso a modelos de visión
- Cuenta de **Google** con acceso a Google Sheets

### Conexiones a configurar en Make.com

1. **Telegram** — Conectar el bot mediante token de BotFather
2. **OpenAI** — Conectar con API Key
3. **Google Sheets** — Conectar cuenta de Google

### Google Sheets

La hoja de cálculo debe tener los encabezados en la **fila 1** con exactamente estos nombres:

```
fecha | importe | iva | categoria | empresa | cif_nif | numero_factura
```

---

## 🚀 Instalación

1. Descarga el archivo `blueprint.json` de este repositorio
2. Accede a Make.com → **Scenarios** → **Create a new scenario**
3. Haz clic en el menú de tres puntos → **Import Blueprint**
4. Sube el archivo `blueprint.json`
5. Configura las conexiones de Telegram, OpenAI y Google Sheets con tus credenciales
6. Activa el escenario

---

## 📱 Cómo usar

1. Abre el bot de Telegram configurado
2. Adjunta la foto del ticket pulsando el clip 📎
3. **⚠️ IMPORTANTE: Envía siempre como archivo/documento**, no como foto

   > Si lo envías como foto normal, Telegram comprime la imagen y la IA no puede leerla correctamente.

4. Espera unos segundos — los datos aparecerán automáticamente en Google Sheets ✅

---

## 🤖 Modelo de IA

- **Modelo:** `gpt-4o-mini-2024-07-18`
- **Capacidad:** Visión (análisis de imágenes)
- **Max tokens:** 500
- **Temperature:** 1

> Si los resultados no son precisos (tickets con letra pequeña o baja calidad), se puede cambiar el modelo a `gpt-4o` para mayor capacidad de lectura, a costa de un mayor coste por operación.

---

## ⚠️ Notas importantes

- **Calidad de imagen:** Asegúrate de que el ticket esté bien iluminado, plano y sin reflejos para obtener los mejores resultados.
- **Formato de envío:** Siempre como 📎 **archivo/documento**, nunca como foto comprimida.
- **Campos ausentes:** Si el ticket no contiene algún dato (como el CIF), el campo se guardará como vacío en la hoja.
- **Idioma:** El prompt está optimizado para tickets en **español**.

---

## 🛠️ Tecnologías

![Make.com](https://img.shields.io/badge/Make.com-6D00CC?style=flat&logo=make&logoColor=white)
![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?style=flat&logo=telegram&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white)
![Google Sheets](https://img.shields.io/badge/Google%20Sheets-34A853?style=flat&logo=google-sheets&logoColor=white)
