# SIGA - Sistema de Controle de Estoque e Patrimônio

## Overview

SIGA (Sistema Integrado de Gestão de Ativos e Estoque) is an enterprise web application designed to modernize and centralize inventory and asset management for organizations. The system enables users to track products (inventory), manage company assets (equipment, furniture), record movements, generate reports, and receive automated alerts for stock levels and asset maintenance.

**Core Capabilities:**
- Real-time inventory monitoring with automatic low-stock alerts
- Asset lifecycle management (location, condition, maintenance history)
- Movement tracking for both inventory and assets
- Role-based access control (5 user roles)
- Dashboard with KPIs and analytics
- Comprehensive reporting system

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework:** React 18 with TypeScript, built using Vite for optimal development experience and production builds.

**Routing:** Wouter (lightweight alternative to React Router) handles client-side navigation with protected routes based on user roles.

**State Management:**
- **Authentication State:** Zustand with persistence middleware for user sessions, stored in localStorage
- **Server State:** TanStack Query (React Query) for data fetching, caching, and synchronization with the backend
- **Form State:** React Hook Form with Zod validation for type-safe form handling

**UI Component Strategy:**
- **Design System:** Material Design principles with custom enterprise theming
- **Component Library:** Radix UI primitives wrapped with shadcn/ui components for accessibility and customization
- **Styling:** Tailwind CSS with custom design tokens defined in CSS variables for theming support
- **Typography:** Inter font family optimized for data-dense interfaces

**Key Design Decisions:**
- Single Page Application (SPA) architecture for fluid user experience
- All API communication via JSON over HTTPS
- Client-side role-based route protection
- Responsive design with mobile-first approach (breakpoint at 768px)

### Backend Architecture

**Framework:** Express.js with TypeScript running on Node.js

**API Design:** RESTful API following resource-based URL patterns (`/api/products`, `/api/assets`, `/api/movements`, etc.)

**Data Access Layer:** 
- **ORM:** Drizzle ORM for type-safe database queries
- **Schema Validation:** Zod schemas generated from Drizzle schemas using `drizzle-zod` for runtime validation
- **Storage Abstraction:** Interface-based storage layer (`IStorage`) allowing for flexible data source implementations

**Authentication & Authorization:**
- JWT-based authentication (currently mock implementation)
- Role-based access control with 5 distinct roles:
  - `ADMINISTRADOR`: Full system access
  - `GESTOR_ESTOQUE`: Inventory management
  - `GESTOR_PATRIMONIAL`: Asset management
  - `EXECUTIVO`: Read-only dashboard and reports
  - `OPERACIONAL`: Basic operations

**Development vs Production:**
- Development: Vite dev server with HMR integrated via middleware
- Production: Static file serving from built assets

**Key Architectural Decisions:**
- Separation of concerns: Routes, storage layer, and business logic are decoupled
- Type sharing between frontend and backend via shared schema definitions
- Middleware-based request logging and error handling
- Raw body preservation for webhook integrations (if needed)

### Data Model

**Core Entities:**

1. **Users**: Authentication, authorization, profile information
2. **Products**: Inventory items with SKU, quantity, min stock levels
3. **Assets**: Company property with patrimony numbers, status, location
4. **Movements**: Transaction records for both products and assets
5. **Categories**: Product classification
6. **Locations**: Physical locations for asset tracking
7. **Alerts**: Automated notifications for stock levels and maintenance

**Relationships:**
- Products → Categories (many-to-one)
- Assets → Locations (many-to-one)
- Movements → Products/Assets (many-to-one, polymorphic via movement type)
- Alerts → Products/Assets (many-to-one)

**Status Enumerations:**
- Asset Status: `EM_USO`, `MANUTENCAO`, `BAIXADO`
- Movement Types: `ENTRADA_PRODUTO`, `SAIDA_PRODUTO`, `MOV_ATIVO`, `MANUTENCAO_ATIVO`, `BAIXA_ATIVO`
- Alert Types: `ESTOQUE_BAIXO`, `ESTOQUE_EXCEDENTE`, `MANUTENCAO_PENDENTE`

## External Dependencies

### Database
- **PostgreSQL**: Primary relational database (via Neon serverless driver `@neondatabase/serverless`)
- **Drizzle Kit**: Database migrations and schema management
- Database URL provided via `DATABASE_URL` environment variable

### UI Libraries
- **Radix UI**: Headless component primitives (@radix-ui/* packages)
- **shadcn/ui**: Pre-built accessible components
- **Recharts**: Data visualization for dashboards and reports
- **Lucide React**: Icon library
- **Embla Carousel**: Carousel/slider functionality

### Form & Validation
- **React Hook Form**: Form state management
- **Zod**: Schema validation for both forms and API requests
- **@hookform/resolvers**: Integration between React Hook Form and Zod

### Development Tools
- **Vite**: Build tool and dev server
- **TypeScript**: Type safety across the stack
- **Tailwind CSS**: Utility-first styling
- **PostCSS & Autoprefixer**: CSS processing

### Third-Party Services
- **Replit Integration**: Development environment plugins (@replit/vite-plugin-*)
- No external SaaS integrations currently configured (ERP, payment processors, etc. are future enhancements)

### Session Management
- **connect-pg-simple**: PostgreSQL session store (configured but not actively used with current JWT approach)

### Utilities
- **date-fns**: Date manipulation and formatting
- **clsx & tailwind-merge**: Conditional className composition
- **class-variance-authority**: Component variant management
- **nanoid**: Unique ID generation