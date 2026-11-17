# Endpoints

Todos van bajo el prefijo `/api`, con JSON. Las rutas protegidas exigen el encabezado `Authorization: Bearer <token>`.

| Método | Ruta | Acceso | Descripción |
|---|---|---|---|
| GET | /api/salud | público | Confirma que la API y la base responden |
| POST | /api/auth/login | público | Inicia sesión y devuelve el JWT |
| POST | /api/auth/registro | admin | Registra un empleado |
| GET | /api/auth/perfil | autenticado | Perfil del usuario del token |
| GET | /api/servicios | autenticado | Lista servicios |
| GET | /api/servicios/:id | autenticado | Detalle de un servicio |
| POST | /api/servicios | admin | Crea un servicio |
| PUT | /api/servicios/:id | admin | Modifica un servicio |
| DELETE | /api/servicios/:id | admin | Elimina un servicio |
| GET | /api/clientes | autenticado | Lista clientes |
| GET | /api/clientes/:id | autenticado | Detalle de un cliente |
| POST | /api/clientes | autenticado | Crea un cliente |
| PUT | /api/clientes/:id | autenticado | Modifica un cliente |
| DELETE | /api/clientes/:id | admin | Elimina un cliente |
| GET | /api/prendas | autenticado | Lista prendas con filtros |
| GET | /api/prendas/:id | autenticado | Detalle de una prenda |
| POST | /api/prendas | autenticado | Registra una prenda |
| PUT | /api/prendas/:id | autenticado | Modifica una prenda |
| DELETE | /api/prendas/:id | admin | Elimina una prenda |
| GET | /api/pedidos | autenticado | Lista pedidos con filtros |
| GET | /api/pedidos/:id | autenticado | Pedido con cliente, prendas, pagos y empleado |
| POST | /api/pedidos | autenticado | Crea un pedido con varias prendas |
| PATCH | /api/pedidos/:id/estado | autenticado | Avanza el estado del pedido |
| GET | /api/pedidos/:id/pagos | autenticado | Lista los pagos de un pedido |
| POST | /api/pedidos/:id/pagos | autenticado | Registra un pago |
| GET | /api/reportes/atrasados | autenticado | Pedidos atrasados |
| GET | /api/reportes/servicios-mas-solicitados | admin | Top 5 de servicios en un rango de fechas |