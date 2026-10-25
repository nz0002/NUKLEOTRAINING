# NUKLEO TRAINING · base del proyecto (fase 1)

Estado real: esquema de base de datos, seguridad, tarifas iniciales y lógica de cálculo/WhatsApp. NO incluye todavía la interfaz Next.js ni el panel /admin (fase 2). Nada de esto se ha probado contra un Supabase real.

## Configurar Supabase
1. Crea un proyecto en supabase.com.
2. SQL Editor: ejecuta `supabase/migrations/001_schema.sql` y luego `002_seed_tarifas.sql`.
3. Authentication → Providers → Email: desactiva "Allow new users to sign up" (evita registros públicos).
4. Authentication → Users → Add user: crea tu usuario con tu correo y una contraseña larga.
5. Hazte administradora (SQL Editor): `insert into admins (user_id) select id from auth.users where email = 'TU_CORREO';`
6. Copia URL y clave anon (Settings → API) a `.env.local` siguiendo `.env.example`.

## Seguridad (ya definida en el esquema)
Lectura pública solo de productos publicados, tramos, precios y contenido publicado. Escritura y borradores solo para quien esté en `admins`. Imágenes: JPG/PNG/WebP, máx. 5 MB, subida solo admin.

## Pruebas
`node --experimental-strip-types tests/pricing.test.ts` (Node 22+): comprueba 24/25, 39/40, 69/70 y la URL de WhatsApp.

## Copias de seguridad
Supabase → Database → Backups (planes de pago) o `pg_dump` con la cadena de conexión; las imágenes, desde Storage. Restaura ejecutando el volcado en un proyecto nuevo.
