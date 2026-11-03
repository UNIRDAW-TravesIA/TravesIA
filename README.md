# TravesIA

Aplicación web de planificación de viajes con IA. A partir de las preferencias del usuario (destino, fechas, presupuesto y estilo de viaje) genera un itinerario día a día en formato timeline.

Proyecto intermodular del ciclo DAW. Todo el código debe ser comprendido y defendible por quien lo integra.

## Interfaz

Layout de tres paneles:

1. Sidebar izquierdo: historial de chats y viajes guardados (colapsable).
2. Zona central: chat interactivo con la IA.
3. Zona derecha: timeline del itinerario, actividades y métricas.

## Equipo

| Persona | Responsabilidad |
|---|---|
| Roberto | Frontend y UI/UX: Angular, Tailwind CSS, diseño visual |
| Vega | Backend e IA: Node.js, Express, prompts, CI/CD |
| Andiee | Base de datos, autenticación y QA: Supabase, Google OAuth, pruebas de carga |

## Stack

- Cliente: Angular 21 (Angular CLI) y Tailwind CSS 4.
- Servidor: Node.js y Express (pendiente de crear).
- Base de datos: PostgreSQL en Supabase.
- Despliegue: Vercel (cliente) y Render (servidor), con deploy automático al hacer merge en `main`.

## Requisitos previos

- [Node.js 24](https://nodejs.org) (incluye npm 11). Comprueba con `node -v`.
- [Git](https://git-scm.com).
- Angular CLI, instalado de forma global:

```bash
npm install -g @angular/cli
```

- Extensiones de VS Code recomendadas:
  - Angular Language Service (`angular.ng-template`)
  - ESLint (`dbaeumer.vscode-eslint`)
  - Prettier (`esbenp.prettier-vscode`)
  - Tailwind CSS IntelliSense (`bradlc.vscode-tailwindcss`)

Recomendado: activa "Format on Save" en VS Code con Prettier como formateador por defecto.

## Puesta en marcha

```bash
git clone https://github.com/UNIRDAW-TravesIA/TravesIA.git
cd TravesIA
git checkout dev
cd client
npm install
npm start
```

La aplicación queda disponible en `http://localhost:4200`.

Cada vez que cambies de rama o hagas `git pull`, ejecuta `npm install` dentro de `client/` por si alguien ha añadido dependencias.

### Comandos del cliente

Se ejecutan siempre dentro de `client/`:

| Comando | Descripción |
|---|---|
| `npm start` | Servidor de desarrollo con recarga automática |
| `npm run build` | Build de producción en `client/dist/client/browser` |
| `npm test` | Tests unitarios con Vitest |

Los comandos `ng ...` solo funcionan dentro de `client/`. Si ves el error "This command is not available when running the Angular CLI outside a workspace", estás en la carpeta equivocada.

### Servidor

Todavía no existe. Cuando se cree, sus comandos serán:

```bash
cd server
npm install
npm run dev
```

Las variables de entorno irán en `server/.env`, que no se sube al repositorio. Se mantendrá un `server/.env.example` con los nombres de las variables sin valores reales.

## Flujo de trabajo con Git

### Ramas

| Rama | Uso |
|---|---|
| `main` | Producción. Cada merge despliega automáticamente. |
| `dev` | Integración. Aquí se juntan las features antes de pasar a producción. |
| `feature/<nombre>` | Una rama por tarea, creada siempre desde `dev`. |

Nunca se hace push directo a `main` ni a `dev`. Todo entra mediante Pull Request.

### Ciclo de una tarea

1. Actualiza `dev` y crea tu rama:

```bash
git checkout dev
git pull origin dev
git checkout -b feature/nombre-descriptivo
```

2. Trabaja y haz commits pequeños y frecuentes:

```bash
git add <archivos>
git commit -m "feat: añade componente de chat"
```

3. Sube la rama:

```bash
git push -u origin feature/nombre-descriptivo
```

4. En GitHub abre un Pull Request con **base `dev`** y **compare tu rama**. Comprueba el desplegable de base antes de crearlo, por defecto GitHub propone `main`.
5. Pide revisión a otro miembro del equipo. Se hace merge cuando haya al menos una aprobación.
6. Tras el merge, borra la rama y vuelve a empezar desde `dev` actualizado.

### Paso a producción

Cuando `dev` esté estable, se abre un Pull Request con **base `main`** y **compare `dev`**. Al hacer merge se dispara el deploy.

### Convención de commits

Formato `tipo: descripción` en español, corto y en imperativo.

| Tipo | Uso |
|---|---|
| `feat` | Nueva funcionalidad |
| `fix` | Corrección de un error |
| `refactor` | Cambio interno sin modificar el comportamiento |
| `docs` | Documentación |
| `chore` | Configuración, dependencias y tareas de mantenimiento |

Ejemplos: `feat: añade timeline de itinerario`, `fix: corrige el scroll del chat`.

### Mantener tu rama al día

Si `dev` avanza mientras trabajas:

```bash
git fetch origin
git merge origin/dev
```

Resuelve los conflictos, si los hay, y continúa.

### Errores habituales

- Hacer commit estando en `dev` o `main`: comprueba con `git branch` en qué rama estás antes de empezar.
- Hacer `git add .` desde una subcarpeta: solo añade esa carpeta. Ejecútalo desde la raíz del repo.
- Subir `node_modules`, `.env` o `dist`: están en `.gitignore`. Si aparecen en `git status`, avisa.

## Convenciones de código

- Documentación y commits en español; identificadores de código en inglés.
- Formato con Prettier y análisis con ESLint antes de cada PR.
- Sin comentarios que expliquen lo obvio. Solo se comenta el porqué de una decisión no evidente.
- Los endpoints que usen un LLM deben forzar una respuesta JSON estricta, sin Markdown ni texto adicional.
- Si se usa IA como apoyo, hay que entender el código que se integra y saber justificarlo en la demo.

Las reglas completas están en [AGENTS.md](AGENTS.md).

## Diseño

| Elemento | Valor |
|---|---|
| Terracota (primario) | `#C6754E` |
| Verde bosque (secundario) | `#323E32` |
| Arena (fondo) | `#E7DDD1` |
| Texto | `#1a1a1a` |
| Títulos | Playfair Display |
| Cuerpo e interfaz | Inter |

## Reuniones

Sesiones de trabajo los sábados de 11:00 a 13:00. Los primeros 15-20 minutos son para la demo de lo realizado y la explicación técnica de las decisiones.
