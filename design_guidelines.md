# SIGA - Design Guidelines
**Sistema de Controle de Estoque e Patrimônio**

## Design Approach
**System Selected**: Material Design + Custom Enterprise Theme  
**Rationale**: Data-heavy enterprise application requiring clear information hierarchy, robust form patterns, and professional table/dashboard components. Material Design provides tested patterns for complex data interactions while maintaining accessibility and scalability.

## Core Design Principles
1. **Information Clarity**: Prioritize data readability over decorative elements
2. **Efficient Navigation**: Minimize clicks to reach critical functions
3. **Status Visibility**: Use color-coded indicators for alerts and inventory levels
4. **Responsive Density**: Comfortable spacing on desktop, compact on mobile

## Typography
- **Primary Font**: Inter (Google Fonts) - excellent for data-dense interfaces
- **Headings**: 
  - H1: text-3xl font-bold (Dashboard titles)
  - H2: text-2xl font-semibold (Section headers)
  - H3: text-lg font-semibold (Card titles, table headers)
- **Body**: text-sm (default for tables, forms, content)
- **Data/Metrics**: text-base font-medium (for KPI numbers)
- **Labels**: text-xs font-medium uppercase tracking-wide (form labels, badges)

## Layout System
**Spacing Units**: Use Tailwind spacing of 2, 3, 4, 6, 8, 12, 16 units
- Component padding: p-4 to p-6
- Section spacing: space-y-6 to space-y-8
- Card gaps: gap-4
- Form field spacing: space-y-3
- Table cell padding: px-4 py-3

**Grid System**:
- Dashboard KPIs: grid-cols-1 md:grid-cols-2 lg:grid-cols-4
- Product/Asset cards: grid-cols-1 md:grid-cols-2 xl:grid-cols-3
- Report layouts: Two-column (chart + metrics): grid-cols-1 lg:grid-cols-3 (2/3 + 1/3 split)

**Container Widths**:
- Main content: max-w-7xl mx-auto
- Forms: max-w-2xl
- Modals: max-w-4xl

## Component Library

### Navigation
- **Sidebar**: Fixed left sidebar (w-64) with collapsible option (w-16 icon-only)
- Logo area at top with SIGA branding
- Role-based menu items with icons (Heroicons)
- Active state: background accent with left border indicator
- Nested menus for sub-sections

### Dashboard Cards
- White background with subtle border (border border-gray-200)
- Rounded corners: rounded-lg
- Header with title + action icon
- Large metric display with trend indicator (up/down arrows)
- Optional sparkline chart below metric
- Shadow on hover: hover:shadow-md transition

### Tables
- Alternating row colors for readability (even:bg-gray-50)
- Sticky header on scroll
- Row hover state: hover:bg-gray-100
- Action column with icon buttons (edit, delete, view)
- Pagination at bottom
- Search and filter toolbar above table
- Status badges in cells (colored pills for inventory levels, asset status)

### Forms
- Floating labels or top-aligned labels
- Input fields: border-gray-300 focus:border-primary focus:ring-2
- Required field indicators (red asterisk)
- Inline validation messages below fields
- Group related fields with subtle dividers
- Action buttons right-aligned at bottom

### Alerts & Notifications
- Toast notifications (top-right): Success (green), Warning (amber), Error (red)
- Badge indicators on sidebar menu items for alerts count
- Alert banner at top of dashboard for critical stock/maintenance issues
- Color-coded alert cards: 
  - Low stock: border-l-4 border-orange-500
  - Maintenance due: border-l-4 border-yellow-500

### Data Visualization
- **Charts** (Recharts):
  - Line charts for trends (consumption over time)
  - Bar charts for comparisons (costs by category)
  - Pie/donut for distributions (asset status breakdown)
- **Color Palette for Charts**:
  - Primary data: #ff5d38 (brand orange)
  - Secondary: #dc7759 
  - Tertiary: #e87350
  - Neutral: grays for reference lines
- Legend below or right of chart
- Tooltips on hover with detailed data

### Buttons
- **Primary**: bg-[#ff5d38] hover:bg-[#e87350] text-white
- **Secondary**: border border-gray-300 hover:bg-gray-50
- **Danger**: bg-red-600 hover:bg-red-700 text-white
- Sizes: Small (px-3 py-1.5 text-sm), Default (px-4 py-2), Large (px-6 py-3)
- Icons: Left-aligned with mr-2 spacing

### Badges & Status Indicators
- Rounded pill shape: rounded-full px-2.5 py-0.5 text-xs font-medium
- **Stock Levels**:
  - Critical/Low: bg-red-100 text-red-800
  - Warning: bg-yellow-100 text-yellow-800
  - Good: bg-green-100 text-green-800
- **Asset Status**:
  - Em Uso: bg-blue-100 text-blue-800
  - Manutenção: bg-orange-100 text-orange-800
  - Baixado: bg-gray-100 text-gray-800

### Modals & Dialogs
- Centered overlay with backdrop (bg-black/50)
- White panel: max-w-2xl for forms, max-w-4xl for complex content
- Header with title and close (X) button
- Content area with scrolling if needed
- Footer with action buttons (Cancel left, Primary right)

## Page-Specific Guidelines

### Login Page
- Centered card on neutral background
- SIGA logo at top
- "INSIDE DAVUS" subtitle below logo
- Username and password fields
- "Entrar" button (full width)
- Clean, professional aesthetic

### Dashboard (Executive/Manager)
- KPI cards in top row (4 metrics)
- Charts in 2-column grid below
- Recent alerts section in sidebar widget
- Quick action buttons prominently placed

### Product/Asset Management
- Search bar + filter dropdowns in toolbar
- Table or card view toggle
- "Cadastrar Novo" button (top-right, prominent)
- Export button for reports

### Reports Page
- Filter panel (left sidebar or collapsible)
- Date range picker
- Chart visualization (main area)
- Summary statistics cards
- "Exportar" button (top-right)

## Animations
Use sparingly:
- Page transitions: fade-in (200ms)
- Dropdown menus: slide-down (150ms)
- Toast notifications: slide-in from right (200ms)
- No animated illustrations or complex motions

## Images
**Hero Section**: Not applicable for this enterprise dashboard
**Icons**: Heroicons throughout (outline style for navigation, solid for emphasis)
**Avatars**: User profile icon in top-right header
**Empty States**: Simple icon + text for empty tables/lists (no illustrations)

---

**Critical Success Factors**:
- Immediate data visibility (no unnecessary scrolling)
- Fast navigation between modules
- Clear visual hierarchy for alerts and critical actions
- Professional, trustworthy appearance suitable for business operations