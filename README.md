
# Taller de Expresiones Regulares - Orca Media

**Taller práctico de Expresiones Regulares con MongoDB**
Un sistema de análisis de datos para prácticas con consultas MongoDB usando regex y operadores lógicos aplicados a casos reales de marketing digital.

---

## 📝 Descripción del Sistema

Este proyecto simula una base de datos para una agencia de marketing digital. Contiene colecciones de clientes, campañas, contenidos, empleados y facturación.
Se usa para aprender a construir consultas eficientes con expresiones regulares (`$regex`) y operadores como `$and`, `$or`, `$size`, `$all`, entre otros, en MongoDB.

---

## 🛠️ Cómo crear la base de datos

1. Abre tu terminal y ejecuta MongoDB (o conecta usando Compass).
2. Crea la base de datos:

   ```js
   use orcaMediaDB
   ```

---

## 📦 Cómo importar los archivos `.json`

Usa el comando `mongoimport` para importar cada colección. Asegúrate de estar en el directorio donde están tus archivos `.json`.

```bash
mongoimport --db orcaMediaDB --collection clientes --file clientes.json --jsonArray
mongoimport --db orcaMediaDB --collection campañas --file campañas.json --jsonArray
mongoimport --db orcaMediaDB --collection contenidos --file contenidos.json --jsonArray
mongoimport --db orcaMediaDB --collection empleados --file empleados.json --jsonArray
mongoimport --db orcaMediaDB --collection facturacion --file facturacion.json --jsonArray
```

---

## 🔍 25 Consultas Documentadas

### Clientes

**Consulta 1**: Buscar clientes cuyo estado comience con "a"

```js
db.clientes.find({estado:{$regex:"^a"}})
```

Filtra clientes de estados como "activo", útil para segmentar clientes con los que se este trabajando en el momento.

**Consulta 2**: Clientes con exactamente 3 servicios contratados

```js
db.clientes.find({serviciosContratados:{$size:3}})
```

Permite identificar clientes con mayor engagement o inversión diversificada.

**Consulta 3**: Emails que terminan en ".co"

```js
db.clientes.find({"contacto.email":{$regex:"\\.co$"}})
```

Útil para diferenciar dominios nacionales de internacionales.

**Consulta 4**: Clientes en industrias con patrón "M..a"

```js
db.clientes.find({industria:{$regex:"^M..a$"}})
```

Filtra industrias con estructura de 4 letras, como "Moda".

**Consulta 5**: Clientes con nombres que consisten en una sola palabra

```js
db.clientes.find({nombre:{$regex:"^\\w+$"}})
```

Ideal para filtrar nombres sin espacios (posiblemente marcas comerciales).

---

### Campañas

**Consulta 6**: Campañas en múltiples canales clave

```js
db.campañas.find({canales:{$all:["YouTube", "Facebook", "Instagram"]}})
```

Identifica campañas multicanal, útiles para medir alcance extendido.

**Consulta 7**: Campañas con presupuesto mínimo de 2 millones

```js
db.campañas.find({total:{$not:{$lt:2000000}}})
```

Permite hacer reportes de alto presupuesto.

**Consulta 8**: Campañas cuyo estado no comienza con "fin"

```js
db.campañas.find({estado:{$regex:"^[^fin]"}})
```

Filtra campañas que no están "finalizadas", útiles para seguimiento activo.

**Consulta 9**: Campañas que no usaron Facebook ni Instagram

```js
db.campañas.find({canales:{$nin:["Facebook", "Instagram"]}})
```

Útil para evaluar desempeño de medios alternativos.

**Consulta 10**: Campañas cuyo estado empieza con "p" y termina con "e"

```js
db.campañas.find({estado:{$regex:"^p\\w+e$"}})
```

Filtra estados como "pendiente", para conocer las campañas que faltan ser completadas.

---

### Contenidos

**Consulta 11**: Contenidos con estatus que empieza con "pub" (case insensitive)

```js
db.contenidos.find({estatus:{$regex:"^pub", $options: "i"}})
```

Filtra contenidos publicados, independientemente de mayúsculas. Util para enconanalizar solo los publicados.

**Consulta 12**: Contenidos con más de 600 likes y menos de 50 comentarios

```js
db.contenidos.find({$and:[{"interacciones.likes":{$gt:600}}, {"interacciones.comentarios":{$lt:50}}]})
```

Muestra publicaciones virales con bajo feedback textual.

**Consulta 13**: Contenidos de plataformas que terminan en "ook"

```js
db.contenidos.find({plataforma:{$regex:"ook$"}})
```

Filtra publicaciones de Facebook o similares.

**Consulta 14**: Contenidos con pocos compartidos o sin comentarios

```js
db.contenidos.find({$or:[{"interacciones.compartidos":{$lt:40}}, {"interacciones.comentarios":{$eq:0}}]})
```

Identifica contenidos con baja interacción social.

**Consulta 15**: Tipos de contenido que terminan en "l"

```js
db.contenidos.find({tipo:{$regex:"^\\w+l$"}})
```

Filtra tipos como "carrusel" o "reel", útil para analítica de formatos.

---

### Empleados

**Consulta 16**: Empleados con solo un cliente asignado

```js
db.empleados.find({clientesAsignados:{$size:1}})
```

Ideal para distribuir mejor la carga entre el equipo.

**Consulta 17**: Empleados con ciertos clientes asignados

```js
db.empleados.find({clientesAsignados:{$in:["GameCampus", "Agroindustrialcenter"]}})
```

Filtra equipos asignados a cuentas clave.

**Consulta 18**: Empleados sin ciertos clientes

```js
db.empleados.find({clientesAsignados:{$nin:["Distribuidor Malayo", "Agroindustrialcenter", "Palmas del Sur"]}})
```

Ayuda a reasignar proyectos sin conflictos.

**Consulta 19**: Empleados con cargos de dos palabras (como "Diseñador Senior")

```js
db.empleados.find({cargo:{$regex:"^[A-Z]\\w+\\s\\w+$"}})
```

Filtra cargos compuestos, útil para jerarquías.

**Consulta 20**: Empleados cuyos nombres comienzan con "Dan"

```js
db.empleados.find({nombre:{$regex:"^Dan"}})
```

Búsqueda rápida por nombre, útil en dashboard de RRHH.

---

### Facturación

**Consulta 21**: Estados de pago que empiezan por "pen" (como "pendiente")

```js
db.facturacion.find({estadoPago:{$regex:"^pen", $options:"i"}})
```

Filtra pagos pendientes, útil para gestión de cobros.

**Consulta 22**: Métodos de pago con formato de dos palabras (como "transferencia bancaria")

```js
db.facturacion.find({metodoPago:{$regex:"^\\w+\\s\\w+$"}})
```

Útil para validar formatos de métodos de pago ingresados.

**Consulta 23**: Facturas altas de desarrollo web

```js
db.facturacion.find({$and:[{monto:{$gt:1600000}},{servicio:"Desarrollo Web"}]})
```

Análisis financiero por servicio de alto valor.

**Consulta 24**: Facturas con monto bajo o marcadas como finalizadas

```js
db.facturacion.find({$or:[{monto:{$lt:1500000}},{estoPago:"finalizado"}]})
```

Útil para distinguir ingresos menores y pagos cerrados.

**Consulta 25**: Métodos de pago que empiecen con "e" y tengan 8 caracteres

```js
db.facturacion.find({metodoPago:{$regex:"^e......o"}})
```

Valida formatos como "efectivo", por longitud y estructura.
