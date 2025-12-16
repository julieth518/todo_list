# 📋 Team To-Do

Aplicación web colaborativa para gestionar tareas en equipo con autenticación de usuarios y filtrado en tiempo real.

## 🚀 Demo en Vivo

- **Frontend**: https://todolistproyec.netlify.app/
- **Backend API**: https://todo-list-bgv1.onrender.com

## ✨ Características Principales

- ✅ **Gestión de Tareas**: Crear, editar, marcar como completadas y eliminar tareas
- 👥 **Multiusuario**: Sistema completo de registro e inicio de sesión
- 🔍 **Búsqueda Inteligente**: Busca tareas por texto o autor con debounce
- 🎯 **Filtros**: Visualiza todas, pendientes o completadas
- 🔒 **Seguridad**: Validación de contraseñas (min 8 caracteres, mayúsculas, minúsculas y caracteres especiales)
- 🎨 **Diseño Moderno**: Interfaz colorida y responsive con gradientes cálidos
- 📱 **Responsive**: Funciona perfectamente en desktop, tablet y móvil

## 🎨 Cambios recientes de estilo (tema)

- Se actualizó la paleta visual del frontend: la aplicación ahora usa una combinación principal de tonos rosados (`rose`) con acentos púrpura (`purple`) en lugar de los tonos ámbar anteriores. También se aplicó un fondo morado claro y texto en negro para mayor contraste.
- Archivos relevantes donde se aplicó el cambio:
    - `frontend/tailwind.config.cjs` (paleta: `rose` y `purple`)
    - `frontend/src/index.css` (estilos globales)
    - Componentes: `src/pages/*`, `src/components/*` (reemplazo de clases `amber-*` → `purple-*` y ajustes de gradientes)

Nota rápida: si ves referencias antiguas a `amber` en `frontend/dist/`, regenera el build (ver sección "Instalación Local" abajo).

## 🛠️ Tecnologías

### Frontend
- React 18
- React Router DOM
- Tailwind CSS
- Axios
- React Toastify
- Vite

### Backend
- NestJS
- Prisma ORM
- MySQL
- JWT para autenticación
- bcrypt para encriptación

### Despliegue
- Frontend: Netlify
- Backend: Render
- Base de Datos: Railway (MySQL)

## 📦 Instalación Local

### Requisitos Previos
- Node.js 18+
- npm o yarn
- MySQL

### 1. Clonar el Repositorio
```bash
git clone https://github.com/tu-usuario/team-todo.git
cd team-todo
```

### 2. Configurar Frontend
```bash
cd frontend
npm install
```

Crear archivo `.env`:
```env
VITE_API_URL=http://localhost:3000
```

Iniciar en modo desarrollo:
```bash
npm run dev
```
El frontend estará en `http://localhost:5173`

Regenerar build de producción / comprobar lint:
```bash
# Generar build (actualiza `frontend/dist` con los últimos cambios de CSS/Tailwind)
npm --prefix frontend run build

# Levantar servidor de desarrollo (hot-reload)
npm --prefix frontend run dev

# Ejecutar ESLint (arregla issues reportados)
npm --prefix frontend run lint
```

### 3. Configurar Backend
```bash
cd backend
npm install
```

Crear archivo `.env`:
```env
DATABASE_URL="mysql://root:password@localhost:3306/teamtodo"
FRONTEND_URL="http://localhost:5173"
PORT=3000
```

Generar Prisma Client y migrar la base de datos:
```bash
npx prisma generate
npx prisma migrate dev
```

Iniciar en modo desarrollo:
```bash
npm run start:dev
```
El backend estará en `http://localhost:3000`

## 📁 Estructura del Proyecto

```
team-todo/
├── frontend/
│   ├── src/
│   │   ├── components/       # Componentes reutilizables
│   │   ├── pages/            # Páginas (Home, Login, Register)
│   │   ├── context/          # AuthContext
│   │   ├── hooks/            # useDebounce
│   │   └── App.jsx
│   └── package.json
│
└── backend/
    ├── src/
    │   ├── auth/             # Autenticación
    │   ├── todos/            # Gestión de tareas
    │   ├── users/            # Gestión de usuarios
    │   └── main.ts
    ├── prisma/
    │   └── schema.prisma     # Esquema de BD
    └── package.json
```

## 🔐 Requisitos de Contraseña

Para registrarse, la contraseña debe cumplir:
- ✅ Mínimo 8 caracteres
- ✅ Al menos una letra mayúscula (A-Z)
- ✅ Al menos una letra minúscula (a-z)
- ✅ Al menos un carácter especial (!@#$%^&*...)

## 📡 API Endpoints

### Autenticación
- `POST /auth/register` - Registrar nuevo usuario
- `POST /auth/login` - Iniciar sesión

### Tareas
- `GET /todos` - Obtener todas las tareas
- `POST /todos` - Crear nueva tarea
- `PATCH /todos/:id` - Actualizar tarea
- `DELETE /todos/:id` - Eliminar tarea

### Usuarios
- `GET /users` - Listar todos los usuarios

## 🚀 Despliegue en Producción

### Frontend (Netlify)
1. Conecta tu repositorio
2. Build command: `npm run build`
3. Publish directory: `dist`
4. Agregar variable: `VITE_API_URL=https://tu-backend.onrender.com`

### Backend (Render)
1. Conecta tu repositorio
2. Build command: `npm install && npx prisma generate`
3. Start command: `npm run start:prod`
4. Agregar variables de entorno:
   - `DATABASE_URL` (URL pública de Railway)
   - `FRONTEND_URL` (URL de Netlify)

### Base de Datos (Railway)
1. Crear proyecto MySQL
2. Copiar la URL pública de conexión
3. Usarla en `DATABASE_URL`

## 🐛 Solución de Problemas

### Error de CORS
Asegúrate de que `FRONTEND_URL` en Render incluya tu dominio de Netlify sin `/` al final.

### Error de Base de Datos
Usa la URL **pública** de Railway (con `shuttle.proxy.rlwy.net`), no la interna (`mysql.railway.internal`).

### Problemas de Login/Registro
Verifica que el backend esté corriendo y que las variables de entorno estén correctamente configuradas.


### Notas sobre lint y cambios recientes

- Después de modificar la paleta y las clases Tailwind, es recomendable ejecutar `npm --prefix frontend run lint`.
- Problemas conocidos que pueden aparecer (pendientes):
    - `frontend/src/context/AuthContext.jsx`: evitar exportar utilidades y componentes en el mismo archivo para mantener compatibilidad con fast-refresh; mover helpers a un archivo aparte si es necesario.
    - `frontend/src/pages/Home.jsx`: puede aparecer una variable `logout` declarada pero no usada — eliminar o usarla según corresponda.
Si quieres, puedo aplicar los fixes automáticos para estos dos puntos.

## Licencia

Este proyecto está licenciado bajo la Licencia MIT - ver el archivo [LICENSE](LICENSE) para más detalles.

### Copyright (c) 2025 Angie Coronado

Se otorgan los permisos siguientes:

1. **Uso:** Se puede usar este software de cualquier forma, incluidos, entre otros, los fines comerciales, sin restricciones.
2. **Copiar y distribuir:** Se puede copiar, modificar, fusionar, publicar, distribuir, sublicenciar y vender copias del software.
3. **Modificar:** Se pueden realizar modificaciones al software, siempre y cuando se incluyan las modificaciones en una distribución del software.
4. **Distribuir copias modificadas:** Se pueden distribuir versiones modificadas del software bajo los mismos términos de la Licencia MIT.

**Limitaciones:**

- No se otorgan garantías de ningún tipo, expresas o implícitas, sobre la adecuación para un propósito particular o la seguridad del software.
- El autor o los titulares de derechos de autor no serán responsables de ningún daño o perjuicio que surja del uso del software.

Este proyecto utiliza otros componentes y bibliotecas que pueden estar bajo diferentes licencias. Asegúrate de consultar las licencias correspondientes de cada uno de ellos.


## 👤 Autor

angie coronado - https://github.com/julieth518/todo_list.git
