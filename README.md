# Proyecto Northwind PostgreSQL - Modificado

Este repositorio contiene una versión modificada de la base de datos Northwind para PostgreSQL, desarrollada como proyecto de curso con nuevas funcionalidades y mejoras.

## 📋 Descripción del Proyecto

La base de datos Northwind ha sido extendida con las siguientes mejoras:

### ✨ Nuevas Funcionalidades

- **Propuestas de alumno**: Agregar funcionalidades para mejorrar un carrito de compras
- **CREATE TABLE shopping_cart **: Esta tabla almacenará los productos que un cliente tiene en su carrito
- **vista carrito_cliente_total**: Vista para mostrar el resumen total del carrito por cliente
- **Crear función vaciar_carrito**: Función para eliminar todos los productos del carrito de un cliente específico 
- **Modificacion tabla products**: Añadir columnas jsonb para caracteristicas dinamicas
- **Vistas**: vw_ventas_mes, vw_ventas_diarias, vw_ventas_empleado, vw_top_productos,vw_top_clientes, vw_ventas_categoria, vw_ventas_pais  
- **Auditoría Completa**: Registro de cambios en productos

## 🛠️ Tecnologías

- **PostgreSQL** 12+ 
- **pgAdmin** (opcional)
- **SQL Dump** para instalación rápida

## 📁 Estructura del Repositorio

```
northwind-postgres-modificado/
├── README.md                          # Este archivo
├── modificado_northwind.sql           # ⭐ DUMP COMPLETO DE LA BD
├── docs/
│   ├── INSTALACION.md                 # Guía de instalación
│   ├── FUNCIONALIDADES.md             # Documentación de mejoras
│   └── CONSULTAS_EJEMPLO.md           # Ejemplos de uso
└── screenshots/
    ├── diagrama_er.png                # Diagrama actualizado
    └── consultas_ejemplo.png          # Capturas de pantalla
```

## 🚀 Instalación Rápida

### Prerrequisitos
- PostgreSQL 12 o superior
- Cliente psql o pgAdmin

### Instalación en 3 pasos

1. **Clonar repositorio**
```bash
git clone https://github.com/tu-usuario/northwind-postgres-modificado.git
cd northwind-postgres-modificado
```

2. **Crear base de datos**
```bash
createdb northwind_curso
```

3. **Restaurar dump completo**
```bash
psql -d northwind_curso -f modificado_northwind.sql
```

¡Y listo! La base de datos estará completamente configurada con datos de ejemplo.

### Alternativa con pgAdmin
1. Crear nueva base de datos llamada `northwind_curso`
2. Click derecho → Restore
3. Seleccionar archivo `modificado_northwind.sql`
4. Ejecutar

## 🔍 Funcionalidades Principales

### 1. Consulta sobre los datos de json
```sql
-- Obtener productos de una categoría específica
SELECT product_id, product_name, caracteristicas_json
FROM products
WHERE caracteristicas_json->>'categoria' = 'Electrónica';

```

### 2. Análisis de Ventas
```sql
-- Ventas por mes con métricas
SELECT * FROM ventas_mensuales 
WHERE mes >= '2024-01-01';
```

### 3. Sistema de Descuentos
```sql
-- Calcular descuento por volumen
SELECT calcular_descuento_volumen(1, 75) as descuento_aplicado;
```

### 4. Top Productos
```sql
-- Productos más vendidos
SELECT * FROM top_productos_vendidos LIMIT 10;
```

## 📊 Nuevas Tablas Añadidas

- `subcategories` - Categorías jerárquicas
- `volume_discounts` - Descuentos por cantidad
- `product_audit` - Auditoría de cambios
- `stock_alerts` - Alertas de inventario

## 📈 Vistas Creadas

- `productos_stock_bajo` - Control de inventario
- `ventas_mensuales` - Análisis temporal
- `top_productos_vendidos` - Ranking de productos
- `analisis_clientes` - Segmentación de clientes

## 🔧 Funciones y Triggers

- **Auditoría automática** en cambios de productos
- **Alertas de stock** cuando baja del mínimo
- **Cálculo de descuentos** por volumen de compra
- **Actualización automática** de timestamps

## 📝 Datos de Prueba

El dump incluye:
- Base Northwind completa original
- 8 subcategorías de ejemplo
- 8 reglas de descuento por volumen
- Configuración de stock mínimo
- Alertas de ejemplo generadas

## 🧪 Validar Instalación

Después de restaurar, ejecuta estas consultas para verificar:

```sql
-- Verificar nuevas tablas
SELECT count(*) FROM subcategories;        -- Debe mostrar 8
SELECT count(*) FROM volume_discounts;     -- Debe mostrar 8
SELECT count(*) FROM stock_alerts;        -- Debe mostrar varias

-- Probar vistas
SELECT * FROM vw_ventas_mes;
SELECT * FROM carrito_cliente_total;

-- Probar función
SELECT calcular_descuento_volumen(1, 100);  -- Debe mostrar 10.00
```

## 📋 Especificaciones Técnicas

- **Versión PostgreSQL**: 12+
- **Tamaño del dump**: ~500KB
- **Total tablas**: 17 (13 originales + 4 nuevas)
- **Total vistas**: 4
- **Total funciones**: 3
- **Triggers**: 1 principal con múltiples eventos

## 👨‍🎓 Información Académica

- **Curso**: Bases de Datos Avanzadas
- **Institución**: [Tu Institución]
- **Autor**: [Tu Nombre]
- **Fecha**: Mayo 2025

## 📞 Soporte

Si tienes problemas con la instalación:

1. Verifica que PostgreSQL esté corriendo
2. Asegúrate de tener permisos para crear BD
3. Revisa que el archivo SQL esté completo
4. Consulta los logs de PostgreSQL para errores

## 🎯 Objetivos de Aprendizaje Demostrados

- ✅ Modificación de esquemas existentes
- ✅ Creación de tablas relacionadas
- ✅ Implementación de triggers
- ✅ Desarrollo de vistas complejas
- ✅ Funciones en PL/pgSQL
- ✅ Optimización con índices
- ✅ Sistemas de auditoría
- ✅ Generación de dumps

---

**Nota**: Este proyecto demuestra conocimientos avanzados en PostgreSQL aplicados sobre la conocida base de datos Northwind, añadiendo funcionalidades empresariales reales.
