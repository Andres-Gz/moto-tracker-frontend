# 💻 Moto Tracker - Frontend

Aplicación web para el sistema de gestión de vehículos personales MotoTracker.

## 📋 Descripción

Frontend desarrollado en **React + TypeScript** que proporciona una interfaz moderna y responsive para:
- Gestión de vehículos personales
- Registro y seguimiento de mantenimientos
- Control de gastos operativos
- Dashboard con estadísticas y gráficas
- Sistema de autenticación

## 🛠️ Stack Tecnológico

- **React:** 18.3.x
- **TypeScript:** 5.3.x
- **Build Tool:** Vite 5.x
- **Routing:** React Router 6.x
- **State Management:** React Query (TanStack Query)
- **HTTP Client:** Axios
- **Styling:** TailwindCSS 3.x
- **Forms:** React Hook Form + Zod
- **Charts:** Recharts
- **Date Handling:** date-fns

## 📁 Estructura del Proyecto

```
src/
├── components/           # Componentes reutilizables
│   ├── common/          # Buttons, Inputs, Cards, Modals
│   ├── layout/          # Header, Sidebar, Footer
│   └── forms/           # Form components específicos
├── pages/               # Páginas principales
│   ├── auth/            # Login, Register
│   ├── dashboard/       # Dashboard principal
│   ├── vehicles/        # CRUD de vehículos
│   ├── maintenances/    # Gestión de mantenimientos
│   └── expenses/        # Gestión de gastos
├── services/            # Llamadas a la API
│   ├── api.ts           # Configuración Axios
│   ├── authService.ts
│   ├── vehicleService.ts
│   ├── maintenanceService.ts
│   └── expenseService.ts
├── hooks/               # Custom React Hooks
│   ├── useAuth.ts
│   ├── useVehicles.ts
│   └── useDebounce.ts
├── context/             # Context API
│   └── AuthContext.tsx
├── types/               # TypeScript interfaces
│   └── index.ts
├── utils/               # Funciones utilitarias
│   ├── formatters.ts
│   └── validators.ts
├── App.tsx
└── main.tsx
```

## 🚀 Quick Start

### Prerrequisitos

- Node.js 18+ 
- npm 9+ o yarn 1.22+

### Instalación

```bash
# Clonar repositorio
git clone https://github.com/Andres-Gz/moto-tracker-frontend.git
cd moto-tracker-frontend

# Instalar dependencias
npm install

# Configurar variables de entorno
cp .env.example .env.local

# Iniciar servidor de desarrollo
npm run dev
```

La aplicación estará disponible en: `http://localhost:5173`

### Variables de Entorno

Crear archivo `.env.local`:

```env
VITE_API_URL=http://localhost:8080/api
VITE_APP_NAME=Moto Tracker
```

## 📦 Scripts Disponibles

```bash
# Desarrollo
npm run dev              # Iniciar servidor de desarrollo

# Build
npm run build            # Compilar para producción
npm run preview          # Preview del build de producción

# Linting y Formateo
npm run lint             # Ejecutar ESLint
npm run format           # Formatear código con Prettier

# Testing
npm run test             # Ejecutar tests con Vitest
npm run test:ui          # Ejecutar tests con UI
npm run coverage         # Generar reporte de coverage
```

## 🎨 Componentes Principales

### Layout
- `Header` - Barra de navegación superior
- `Sidebar` - Menú lateral (desktop)
- `Footer` - Pie de página
- `Layout` - Wrapper principal

### Auth
- `LoginForm` - Formulario de inicio de sesión
- `RegisterForm` - Formulario de registro
- `ProtectedRoute` - HOC para rutas protegidas

### Vehicles
- `VehicleList` - Lista de vehículos
- `VehicleCard` - Tarjeta de vehículo
- `VehicleForm` - Formulario crear/editar
- `VehicleDetails` - Vista detallada

### Dashboard
- `DashboardStats` - Tarjetas de estadísticas
- `ExpenseChart` - Gráfica de gastos
- `MaintenanceTimeline` - Línea de tiempo
- `RecentActivity` - Actividad reciente

## 🔐 Autenticación

El flujo de autenticación utiliza:
- **JWT tokens** almacenados en `localStorage`
- **AuthContext** para estado global de autenticación
- **Axios interceptors** para agregar token automáticamente

```typescript
// Uso del AuthContext
import { useAuth } from '@/hooks/useAuth';

function MyComponent() {
  const { user, login, logout, isAuthenticated } = useAuth();
  
  // ...
}
```

## 📡 Servicios API

Todos los servicios están en `/src/services`:

```typescript
// Ejemplo de uso
import vehicleService from '@/services/vehicleService';

const vehicles = await vehicleService.getAll();
const vehicle = await vehicleService.create(data);
```

### React Query Integration

```typescript
import { useQuery, useMutation } from '@tanstack/react-query';

// Obtener vehículos
const { data, isLoading } = useQuery({
  queryKey: ['vehicles'],
  queryFn: vehicleService.getAll
});

// Crear vehículo
const createMutation = useMutation({
  mutationFn: vehicleService.create,
  onSuccess: () => {
    queryClient.invalidateQueries({ queryKey: ['vehicles'] });
  }
});
```

## 🎨 Estilos con TailwindCSS

### Configuración personalizada

Ver `tailwind.config.js` para:
- Paleta de colores personalizada
- Breakpoints responsivos
- Plugins adicionales

### Convenciones de clases

- Usar clases utilitarias de Tailwind
- Evitar CSS custom cuando sea posible
- Componentes complejos pueden usar CSS Modules

## 🧪 Testing

```bash
# Ejecutar tests
npm run test

# Ejecutar en modo watch
npm run test:watch

# Generar coverage
npm run coverage
```

### Estructura de tests

```
src/
├── components/
│   └── Button/
│       ├── Button.tsx
│       └── Button.test.tsx
└── pages/
    └── Dashboard/
        ├── Dashboard.tsx
        └── Dashboard.test.tsx
```

## 🐳 Docker

### Desarrollo

```bash
docker build -t moto-tracker-frontend .
docker run -p 5173:5173 moto-tracker-frontend
```

### Producción

```bash
docker build -f Dockerfile.prod -t moto-tracker-frontend:prod .
docker run -p 80:80 moto-tracker-frontend:prod
```

## 📱 Responsive Design

La aplicación es totalmente responsive con breakpoints:

- **Mobile:** < 640px
- **Tablet:** 640px - 1024px
- **Desktop:** > 1024px

## 🚀 Deploy

### Vercel (Recomendado)

1. Conectar repositorio con Vercel
2. Configurar variables de entorno
3. Deploy automático en cada push a `main`

```bash
# Deploy manual
npm run build
vercel --prod
```

### Netlify

```bash
# Build command
npm run build

# Publish directory
dist

# Environment variables
VITE_API_URL=https://api.mototracker.com/api
```

## 🔧 Configuración TypeScript

El proyecto usa TypeScript estricto con las siguientes opciones:

```json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true
  }
}
```

## 📊 Performance

### Optimizaciones implementadas:

- **Code splitting** por rutas
- **Lazy loading** de componentes pesados
- **React Query caching** para reducir llamadas
- **Memoization** con `useMemo` y `useCallback`
- **Optimized images** con lazy loading

## 🎯 Rutas de la Aplicación

```
/                      → Redirect a /dashboard o /login
/login                 → Página de login
/register              → Página de registro
/dashboard             → Dashboard principal
/vehicles              → Lista de vehículos
/vehicles/new          → Crear vehículo
/vehicles/:id          → Detalle de vehículo
/vehicles/:id/edit     → Editar vehículo
/maintenances          → Historial de mantenimientos
/expenses              → Historial de gastos
/profile               → Perfil de usuario
```

## 📚 Documentación Adicional

- [Documentación completa del proyecto](https://github.com/Andres-Gz/moto-tracker-docs)
- [API Backend](https://github.com/Andres-Gz/moto-tracker-backend)
- [Guía de estilos](./docs/STYLE_GUIDE.md)

## 🤝 Contribución

1. Fork el proyecto
2. Crear feature branch (`git checkout -b feature/nueva-funcionalidad`)
3. Commit cambios (`git commit -m 'feat: agregar nueva funcionalidad'`)
4. Push al branch (`git push origin feature/nueva-funcionalidad`)
5. Crear Pull Request

### Convenciones de Commits

Seguimos [Conventional Commits](https://www.conventionalcommits.org/):

- `feat:` - Nueva funcionalidad
- `fix:` - Corrección de bug
- `docs:` - Cambios en documentación
- `style:` - Formateo, punto y coma faltantes, etc
- `refactor:` - Refactorización de código
- `test:` - Agregar tests
- `chore:` - Mantenimiento

## 📄 Licencia

MIT License - ver [LICENSE](LICENSE) para más detalles

## 👨‍💻 Autor

**Andre García**
- GitHub: [@Andres-Gz](https://github.com/Andres-Gz)

---

⭐ Si te gusta el proyecto, dale una estrella en GitHub!
