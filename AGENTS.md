# AGENTS.md - TravesIA Workspace Context & Guidelines

## 1. Project Summary & Architecture
TravesIA es una aplicación web de planificación de viajes con IA. Convierte las preferencias del usuario (destino, fechas, presupuesto, estilo) en itinerarios día a día en formato timeline.

### Layout de 3 Paneles Concurrente
1. **Sidebar Izquierdo:** Historial de chats y viajes guardados (colapsable).
2. **Zona Central:** Interfaz de chat interactiva con la IA.
3. **Zona Derecha:** Timeline del itinerario generado, actividades y métricas.

---

## 1.1 Academic Context
- Somos estudiantes de **DAW (Desarrollo de Aplicaciones Web)** y este es un **proyecto intermodular**: se evalúa tanto el resultado como la comprensión del equipo.
- Se puede usar IA como apoyo, pero **todo el código debe poder explicarse por quien lo entrega**: qué hace, cómo funciona, por qué se eligió esa solución frente a otras y qué alternativas se descartaron.
- Al proponer código o configuración, el agente debe explicar el razonamiento de forma breve y didáctica, evitar soluciones opacas o "mágicas" y preferir la opción más sencilla que cumpla el requisito.
- El agente no debe introducir librerías, patrones o abstracciones que el equipo no pueda justificar en la defensa del proyecto sin antes proponerlos y explicarlos.
- Cada miembro debe poder defender en la demo cualquier parte del código que haya integrado.

---

## 2. Team & Role Distribution
- **Roberto (Frontend & UI/UX Lead):** Angular, Tailwind CSS, Penpot, Lighthouse, tipografía y diseño visual.
- **Vega / User (Backend & AI Integration Lead):** Node.js, Express REST API, prompt engineering, GitHub Org, Vercel CI/CD, Prometheus.
- **Andiee (Database, Auth & QA Lead):** Supabase (PostgreSQL / pgvector), Google OAuth, testing de carga con Artillery.io.

---

## 3. Design System & Brand Identity

### Color Palette
- **Terracota / Primario:** `#C6754E`
- **Verde Bosque / Secundario:** `#323E32`
- **Arena / Terciario (Fondo):** `#E7DDD1`
- **Texto / Oscuro:** `#1a1a1a`

### Typography Hierarchy
- **Headers / Serif:** `Playfair Display` (serif)
  - `h1`: 2.441rem (39px) / line-height: 1.2
  - `h2`: 1.953rem (31px) / line-height: 1.25
  - `h3`: 1.563rem (25px) / line-height: 1.3
  - `h4`: 1.25rem (20px) / line-height: 1.4
- **Body & UI / Sans-serif:** `Inter` (sans-serif)
  - `p`: 1.0rem (16px) / line-height: 1.5
  - `small` / `.caption`: 0.8rem (13px) / line-height: 1.4

---

## 4. Tech Stack & Infrastructure
- **Monorepo Structure:**
  - `client/`: Angular CLI + Tailwind CSS (Google Fonts: Playfair Display + Inter).
  - `server/`: Node.js + Express REST API + Supabase JS Client.
- **Versiones:** Node 24, npm 11, Angular 21 (Angular CLI), Tailwind CSS 4 (plugin `@tailwindcss/postcss`).
- **Calidad de código:** ESLint + Prettier (configuración compartida en el repo) y Vitest para tests unitarios del cliente.
- **Idioma de la UI:** Español.
- **Database:** PostgreSQL en Supabase.
- **Deployment:** Vercel (Auto-deploy al realizar merge en `main`).
- **Monitoring & QA:** Lighthouse (Front), Prometheus (Back), Artillery.io (Pruebas de carga).

---

## 5. Development Commands

### Client (Angular)
- Install: `cd client && npm install`
- Serve: `cd client && npm start` (o `ng serve`)
- Build: `cd client && npm run build`

### Server (Express)
- Install: `cd server && npm install`
- Dev Mode: `cd server && npm run dev` (`nodemon index.js`)
- Start: `cd server && npm start`

---

## 6. Development Rules & Guidelines
- **Git Branching:** `main` (producción), `dev` (integración), `feature/<nombre>` (ej. `feature/backend-express-setup`). Las claves de Jira (`TRAV-X`) en el nombre de la rama o commits son opcionales.
- **Strict JSON Enforcement:** Todos los endpoints que consuman APIs de LLM deben obligar a la IA a responder un objeto JSON estricto sin bloques Markdown ni texto explicativo adicional.
- **No AI Signatures:** El código generado debe ser limpio, modular, estilo senior full-stack, sin emojis innecesarios ni comentarios redundantes.
  - Sin comentarios que narren lo obvio (`// importa express`, `// crea el servidor`), sin banners decorativos, sin `TODO` genéricos ni explicaciones tipo tutorial dentro del código.
  - Solo se comenta el "por qué" de una decisión no evidente, de forma breve y en el idioma del proyecto.
  - Nombres de variables y funciones descriptivos; el código debe explicarse solo.
  - Sin atribuciones a IA en el código, README ni mensajes de commit (sin `Co-Authored-By` de herramientas).
  - La explicación didáctica va en el chat con el agente o en la documentación, nunca dentro del código entregado.
- **Idioma:** Documentación y mensajes de commit en español; identificadores de código en inglés.
- **Commits:** Mensajes en formato convencional (`feat:`, `fix:`, `chore:`, `docs:`, `refactor:`), cortos y en imperativo.
- **Flujo de integración:** Nunca se hace push directo a `main` ni a `dev`; todo entra mediante Pull Request desde `feature/*` con al menos una revisión de otro miembro.
- **Secretos:** Las claves (Supabase, LLM, OAuth) van en variables de entorno; `.env` está en `.gitignore` y se mantiene un `.env.example` sin valores reales.
- **Team Sync Dynamics:** Sesiones de trabajo los sábados de 11:00 a 13:00. Los primeros 15-20 minutos se destinan a la demo del trabajo realizado y la explicación técnica de las decisiones.