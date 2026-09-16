# GIAN · Agenda

Agenda de GIAN Producciones Inteligentes para gestionar clientes, pedidos y reuniones.

## Funciones

- Fichas de clientes y su historial vinculado.
- Pedidos por orden de registro, servicio, estado, prioridad, presupuesto y fecha de entrega.
- Reuniones con fecha, hora de inicio y fin, domicilio, modalidad y motivo.
- Avisos sonoros a 30 y 10 minutos; exportación al calendario con ambos recordatorios.
- Exportación de registros en JSON.
- Identidad visual con el logo GIAN, azul noche, cian, violeta y verde neón.

Los avisos sonoros requieren activar el sonido y mantener abierta la agenda con el dispositivo encendido. Para reuniones con el navegador cerrado, importar el archivo de calendario y verificar sus notificaciones.

## Estado

Aplicación construida y probada localmente. Publicación web pendiente. La versión actual guarda los datos en D1 y utiliza el inicio de sesión de Sites. La conexión con Supabase está pendiente de seleccionar y autorizar el proyecto de GIAN; todavía no está activa.

Este repositorio contiene código fuente, no un instalador de Windows. No incluye bases de datos, registros de clientes, contraseñas ni archivos de entorno privados.

## Desarrollo

Requiere Node.js 22.13 o posterior.

```sh
npm ci
npm run build
npm run dev
```

Para preparar la base de datos local, después del primer build:

```sh
node --import ./scripts/sites-env.mjs ./node_modules/wrangler/bin/wrangler.js d1 execute DB --local --config dist/server/wrangler.json --persist-to .wrangler/state --file drizzle/0000_right_invisible_woman.sql
```

Aplicar esa migración solo una vez en cada base local nueva. Abrir la dirección que informa el servidor. El enlace de inicio de sesión local usa una cuenta simulada exclusivamente para desarrollo. La autenticación real la proporciona Sites al publicar.

## Publicación y seguridad

La carpeta `.openai` identifica el sitio ya creado. Reutilizar su identificador al continuar la publicación. No desplegar este servidor en otro proveedor sin configurar autenticación fiable: los encabezados de identidad deben proceder del servicio de confianza, nunca directamente del visitante.

No subir `.env`, `.dev.vars`, `.wrangler`, copias de datos, credenciales o claves secretas. Las claves secretas de Supabase deben quedar únicamente en variables del servidor.
