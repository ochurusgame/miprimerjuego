# 📦 Módulo de Inventario, Control de Ventas y Finanzas

Documentación detallada del módulo de gestión financiera e inventario en tiempo real para **React Native / Expo** con base de datos local **SQLite** e integración con la **API de Mercado Libre**.

---

## 📊 1. Lógica Financiera e Inventario (Modelo Excel)

Este módulo automatiza y traslada las hojas de cálculo operativas (`Octubre.xlsx` / `TablaInventario` / `Reportes`):

* **Capital Disponible para Reinvertir:** Muestra en todo momento el flujo líquido disponible resultante de:
  $$\text{Capital Reinversión} = \text{Costo Base de Mercancía Vendida (Recuperación)} + \text{Ganancia Neta Real}$$
* **Cálculo de Margen Neto:**
  $$\text{Ganancia Neta} = \text{Precio Venta Bruto} - \text{Comisión Canal (ML/TikTok)} - \text{Costo Base del Producto}$$
* **Desglose Multibodega:** Separación explícita entre **📦 Bodega Local** (gestionada directamente por el vendedor) y **⚡ Mercado Libre Full** (bodegas automatizadas de Mercado Envíos).

---

## 💾 2. Esquema de Base de Datos SQLite (`src/database/db.ts`)

Las tablas almacenan el catálogo de productos con sus identificadores de Mercado Libre (`ml_item_id`), precios mínimos y existencias desglosadas por ubicación.

```sql
PRAGMA foreign_keys = ON;

-- Tabla de Productos e Inventario (Bodega vs Full)
CREATE TABLE IF NOT EXISTS products (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  ml_item_id TEXT,
  name TEXT NOT NULL,
  category TEXT NOT NULL,
  cost_price REAL NOT NULL,
  stock_local INTEGER NOT NULL DEFAULT 0,
  stock_full INTEGER NOT NULL DEFAULT 0,
  min_price REAL NOT NULL
);

-- Tabla de Registro de Ventas
CREATE TABLE IF NOT EXISTS sales (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  ml_order_id TEXT UNIQUE,
  date TEXT NOT NULL,
  product_id INTEGER,
  channel_name TEXT NOT NULL,
  quantity INTEGER NOT NULL,
  gross_price REAL NOT NULL,
  cost_price REAL NOT NULL,
  net_profit REAL NOT NULL,
  commission REAL NOT NULL,
  is_full INTEGER DEFAULT 0,
  FOREIGN KEY (product_id) REFERENCES products (id)
);
📱 3. Componentes Visuales y Módulos Desarrollados
💵 A. Resumen Financiero (src/screens/DashboardScreen.tsx)
Capital Disponible para Reinvertir: Tarjeta principal que consolida el dinero recuperado por mercancía vendida más las utilidades netas.

Métricas Globales: Indicadores en tiempo real de Ventas Brutas y Ganancia Neta.

Rendimiento por Canal: Lista dinámica que clasifica ingresos y piezas vendidas por canal (Mercado Libre, TikTok Shop).

📦 B. Gestión de Inventario (src/screens/InventoryScreen.tsx)
Stock por Ubicación: Visualización independiente de unidades en Bodega Local y Mercado Libre Full.

Edición Rápida: Modal para ajustar existencias y actualizar el Costo Base sin necesidad de recargar la aplicación.

Alta de Productos: Registro de nuevos artículos con su ID de Mercado Libre (ml_item_id), categoría y precio mínimo de venta.

⚡ C. Servicio de Integración API (src/services/mercadolibre.ts)
Procesa los eventos de ventas entrantes (orders/search).

Detecta automáticamente si el tipo de envío es Full (fulfillment) o Bodega Local (drop_shipping), descontando la pieza de la columna correspondiente en SQLite y actualizando el Dashboard al instante.
