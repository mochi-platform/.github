# Mochi Platform 🍡

**Mochi** es una plataforma de productividad personal diseñada 100% para mujeres estudiantes. Combina planificación académica inteligente, seguimiento de bienestar, rutinas de ejercicio, cocina con IA y gamificación en un ecosistema cohesionado.

---

## Repositorios

| Repo | Descripción | Stack principal |
|---|---|---|
| [`mochi-mobile`](https://github.com/siramong/mochi-mobile) | Aplicación Android (e iOS futuro) | Expo · React Native · NativeWind |

---

## La visión

La mayoría de las apps de productividad están diseñadas de forma genérica o pensadas para hombres. Mochi parte de una premisa distinta: **el cuerpo y los ciclos de una mujer importan**.

La app sincroniza datos de salud (ciclo menstrual vía Health Connect), adapta las recomendaciones de estudio y ejercicio a cada fase del ciclo, y acompaña a la usuaria con una personalidad cálida, sin presión, que celebra cada avance.

---

## Módulos del producto

```
┌─────────────────────────────────────────────────────────┐
│                     Mochi Mobile                        │
├──────────────┬──────────────┬───────────────┬───────────┤
│   Estudio    │   Ejercicio  │    Hábitos    │  Cocina   │
│  (bloques,   │  (rutinas,   │  (seguimiento │  (recetas │
│  Pomodoro,   │   player,    │   diario,     │   con IA, │
│  flashcards, │   logros)    │   rachas)     │   modo    │
│  compañera   │              │               │  cocina)  │
│  IA)         │              │               │           │
├──────────────┴──────────────┴───────────────┴───────────┤
│         Bienestar: mood · gratitud · energía            │
│         Ciclo menstrual (Health Connect)                │
├─────────────────────────────────────────────────────────┤
│   Mochi Duo™: espacio compartido con pareja             │
│   Gamificación: puntos · niveles · logros · vales       │
│   Weekly Planner: sugerencias proactivas con IA         │
├─────────────────────────────────────────────────────────┤
│          Monetización: créditos IA · Premium            │
└─────────────────────────────────────────────────────────┘
```

---

## Infraestructura compartida

| Capa | Servicio |
|---|---|
| Base de datos | Supabase (PostgreSQL + RLS) |
| Autenticación | Supabase Auth (email + Google OAuth) |
| IA | OpenRouter (nvidia/nemotron, gemini-2.0-flash) |
| Imágenes | Unsplash API |
| Anuncios | Google AdMob (rewarded ads) |
| Suscripciones | RevenueCat + Google Play Billing |
| Builds | EAS (Expo Application Services) |
| CI/CD | GitHub Actions |
| Distribución | Google Play Store |

---

## Principios de ingeniería

**Seguridad primero**
Todas las tablas tienen RLS habilitado. El cliente nunca usa service role. La lógica de privilegios y límites se valida en el backend (funciones SECURITY DEFINER).

**IA responsable**
Las llamadas a OpenRouter pasan por un sistema de créditos con límites por plan (free/premium) y validación server-side. Los modelos tienen fallback automático y retry con backoff.

**TypeScript estricto**
Sin `any`. Sin `.js` en código de app. Tipos de ciclo menstrual siempre en español como fuente de verdad.

**UX para mujeres**
Copy 100% en español. Tono cálido, sin culpa, sin presión. Sin emojis en UI (Ionicons). Recomendaciones adaptadas a la fase del ciclo. El sistema de gamificación celebra constancia, no perfección.

---

## Stack de desarrollo

```
Runtime        Node.js 20+
Package mgr    pnpm (workspaces)
Mobile         Expo SDK 55 · React Native 0.83
Estilos        NativeWind v4 (Tailwind v3 syntax)
Animaciones    react-native-reanimated 4.x
Backend        Supabase (self-hosted schema via CLI)
Builds         EAS CLI 18.x
CI             GitHub Actions
```

---

## Estructura de un repositorio de app

```
app/                    → Pantallas (Expo Router)
src/
  core/providers/       → Contextos globales (sesión, ciclo, módulos)
  features/[feature]/   → Componentes + hooks por dominio
  shared/
    components/         → UI reutilizable
    hooks/              → Hooks compartidos
    lib/                → Clientes (ai, supabase, notifications, gamification)
    types/              → Tipos centralizados
plugins/                → Config plugins nativos (Expo)
docs/                   → Documentación de features planificadas
```

---

## Metodología de features

Cada feature nueva pasa por:

1. **Documento de diseño** en `docs/[platform]/planned/` — schema SQL, wireframe de flujo, criterios de aceptación.
2. **Migración SQL** con RLS + GRANTs explícitos antes de tocar código cliente.
3. **Implementación** siguiendo convenciones del proyecto.
4. **Review** con checklist (tipado, RLS, copy en español, async/await, gamificación).

---

## Equipo

| Rol | Persona |
|---|---|
| Fundadora & Product | Doménica |
| Ingeniería | Doménica + Copilot Agents |

---

## Contacto

- Sitio: [mochi.siramong.tech](https://mochi.siramong.tech)
- Soporte: hola@siramong.tech

---

© Siramong. Todos los derechos reservados.
