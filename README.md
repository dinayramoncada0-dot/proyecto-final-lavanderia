# SIGLA: Sistema de Gestión para Lavandería

Base de datos y API REST para administrar una lavandería: clientes, prendas, pedidos con varios servicios, pagos y reportes.

## Integrantes

- [Dinayra Gisselle Moncada Cerrato 20211020276]
- [Gerson Uziel Izaguirre Rodas 20231002835]
- [Raul Fernando Cruz Flores 20201000572]


## Hito H1: Diseño

| Entregable | Archivo |
|---|---|
| Diagrama entidad-relación | `modelo-er.png` |
| Script SQL | `esquemalav.sql` |
| Endpoints de la API | `__Endpoints.md` |

## Modelo entidad-relación

![Modelo ER](modelo-er.png)

La base de datos `sigla` tiene 7 tablas:

| Tabla | Descripción |
|---|---|
| `usuarios` | Empleados que inician sesión (rol `admin` u `operador`, contraseña con bcrypt) |
| `servicios` | Catálogo de servicios (lavado, planchado, tintorería...), cobrados por kilo o por unidad |
| `clientes` | Catálogo de clientes, con identidad única |
| `prendas` | Prendas de cada cliente, con código de etiqueta único y estado (`recibida`, `en_proceso`, `entregada`) |
| `pedidos` | Cabecera del pedido: cliente, empleado, fechas, estado y total |
| `pedido_detalle` | Líneas del pedido (prenda + servicio aplicado). Guarda el precio vigente al momento del pedido |
| `pagos` | Uno o varios pagos por pedido (efectivo, tarjeta o transferencia) |

Al crear un pedido se escriben `pedidos`, `pedido_detalle` y `prendas` en la misma transacción.

## Endpoints

Todos van bajo el prefijo `/api`, con JSON. Las rutas protegidas exigen el encabezado `Authorization: Bearer <token>`. El detalle completo está en `__Endpoints.md`.

| Recurso | Rutas | Acceso |
|---|---|---|
| Salud | `GET /api/salud` | público |
| Autenticación | `POST /api/auth/login` | público |
| | `POST /api/auth/registro` | admin |
| | `GET /api/auth/perfil` | autenticado |
| Servicios | `GET /api/servicios`, `GET /api/servicios/:id` | autenticado |
| | `POST`, `PUT /:id`, `DELETE /:id` | admin |
| Clientes | `GET`, `GET /:id`, `POST`, `PUT /:id` | autenticado |
| | `DELETE /api/clientes/:id` | admin |
| Prendas | `GET`, `GET /:id`, `POST`, `PUT /:id` | autenticado |
| | `DELETE /api/prendas/:id` | admin |
| Pedidos | `GET /api/pedidos`, `GET /api/pedidos/:id` | autenticado |
| | `POST /api/pedidos` (varias prendas) | autenticado |
| | `PATCH /api/pedidos/:id/estado` | autenticado |
| Pagos | `GET`, `POST /api/pedidos/:id/pagos` | autenticado |
| Reportes | `GET /api/reportes/atrasados` | autenticado |
| | `GET /api/reportes/servicios-mas-solicitados` | admin |

## Base de datos

Para crear la base y cargar los datos de catálogo, ejecuta el script en MySQL:

```bash
mysql -u root -p < esquemalav.sql
```

Los usuarios con contraseña bcrypt los carga el script `semilla.js`.
