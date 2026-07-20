# 💠 Mi Flujo Personal

Gestor de finanzas personales en un **solo archivo HTML**. Funciona sin conexión, sin instalar nada y sin servidores: todos tus datos se guardan de forma privada en tu propio navegador (`localStorage`).

## ✨ Funcionalidades

- **💵 Ingresos** — sueldos, freelance, rentas, dividendos (con opción de recurrente mensual).
- **📌 Gastos fijos** — renta, servicios, suscripciones, créditos, con **día de pago** para alertas.
- **🛒 Gastos variables** — compras, comida, transporte, ocio, por categoría.
- **📈 Cuentas de inversión** — aportado vs valor actual y **% de rendimiento**.
- **💳 Créditos y préstamos** — seguimiento **mes a mes** de la deuda pendiente, cuotas pagadas, plan de amortización y fecha estimada de término.
- **🎯 Plan de ahorro y metas** — progreso, aportes y **proyección de fecha** de cumplimiento.
- **🔔 Alertas de vencimientos** — pagos próximos y vencidos calculados automáticamente + recordatorios manuales.
- **☁️ Sincronización en la nube (Firebase)** — inicia sesión con Google y tus datos se guardan y sincronizan automáticamente entre todos tus dispositivos.

### Extras
- 📊 Dashboard con selector de mes, flujo neto y tasa de ahorro.
- 📉 Gráfico de barras (ingresos vs gastos, 6 meses) y 🍩 dona por categoría.
- 🧮 Regla **50/30/20** y ❤️ puntaje de **salud financiera** con consejos.
- 🌓 Modo claro/oscuro y 🌎 multi-moneda (MXN, COP, ARS, USD, EUR, etc.).
- 💾 Respaldo: exportar/importar **JSON** y exportar **CSV**.
- ✨ Datos de ejemplo con un clic.

## 🚀 Cómo usarlo

**Opción A — Local:** descarga `flujo-personal.html` y ábrelo con doble clic en tu navegador.

**Opción B — Como sitio web (GitHub Pages):**
1. En este repo ve a **Settings → Pages**.
2. En *Build and deployment*, en *Source* elige **Deploy from a branch**.
3. Selecciona la rama `main` y carpeta `/ (root)`, guarda.
4. En 1-2 minutos tendrás una URL pública (ej. `https://juznald-cyber.github.io/FLUJO-PERSONAL/`) que abre el `index.html` automáticamente.

## ☁️ Sincronización automática en la nube (opcional, con Firebase)

Por defecto la app guarda todo en el navegador (`localStorage`). Si quieres abrirla desde **cualquier computadora** y que **los cambios se guarden siempre** de forma automática, conecta Firebase (plan gratuito de Google):

### Configuración paso a paso
1. Entra a [console.firebase.google.com](https://console.firebase.google.com) y crea un proyecto nuevo (gratis).
2. **Build → Authentication → Sign-in method:** activa el proveedor **Google**.
3. **Build → Firestore Database:** crea la base de datos (modo producción).
4. **Project settings (⚙️) → Your apps:** crea una app **Web** (`</>`) y copia los valores de `firebaseConfig` (`apiKey`, `authDomain`, `projectId`, `appId`, etc.).
5. Abre la app → **⚙️ Configuración → ☁️ Sincronización en la nube**, pega esos valores y pulsa **Guardar configuración**.
6. Pulsa **Conectar con Google** e inicia sesión. Desde ese momento, cualquier cambio se guarda en la nube y aparece en tus demás dispositivos al iniciar sesión con la misma cuenta.
7. Si publicas la app con GitHub Pages, agrega tu dominio en **Authentication → Settings → Authorized domains** (por ejemplo `juznald-cyber.github.io`).

### Reglas de seguridad de Firestore (impórtantes)
En **Firestore → Rules**, pega esto para que cada usuario solo pueda leer/escribir sus propios datos:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /finanzas/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

## 🔒 Privacidad

- **Sin nube:** todo vive únicamente en el navegador donde abres la app.
- **Con Firebase:** tus datos se guardan en **tu propio** proyecto de Firebase, bajo tu cuenta de Google, protegidos por las reglas de seguridad de arriba. Nadie más que tú tiene acceso.
- Siempre puedes usar **⚙️ Configuración → Exportar JSON** para respaldar o mover tu información manualmente.
