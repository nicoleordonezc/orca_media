clientes

db.clientes.find({estado:{$regex:"^a"}}) 
db.clientes.find({serviciosContratados:{$size:3}})
db.clientes.find({"contacto.email":{$regex:"\\.co$"}})
db.clientes.find({industria:{$regex:"^M..a$"}})
db.clientes.find({nombre:{$regex:"^\\w+$"}})


campañas

db.campañas.find({canales:{$all:["YouTube", "Facebook", "Instagram"]}})
db.campañas.find({total:{$not:{$lt:2000000}}})
db.campañas.find({estado:{$regex:"^[^fin]"}})
db.campañas.find({canales:{$nin:["Facebook", "Instagram"]}})
db.campañas.find({estado:{$regex:"^p\\w+e$"}})

contenidos

db.contenidos.find({estatus:{$regex:"^pub", $options: "i"}})
db.contenidos.find({$and:[{"interacciones.likes":{$gt:600}}, {"interacciones.comentarios":{$lt:50}}]})
db.contenidos.find({plataforma:{$regex:"ook$"}})
db.contenidos.find({$or:[{"interacciones.compartidos":{$lt:40}}, {"interacciones.comentarios":{$eq:0}}]})
db.contenidos.find({tipo:{$regex:"^\\w+l$"}})

empleados

db.empleados.find({clientesAsignados:{$size:1}})
db.empleados.find({clientesAsignados:{$in:["GameCampus", "Agroindustrialcenter"]}})
db.empleados.find({clientesAsignados:{$nin:["Distribuidor Malayo", "Agroindustrialcenter", "Palmas del Sur"]}})
db.empleados.find({cargo:{$regex:"^[A-Z]\\w+\\s\\w+$"}})
db.empleados.find({nombre:{$regex:"^Dan"}})

facturacion

db.facturacion.find({estadoPago:{$regex:"^pen", $options:"i"}})
db.facturacion.find({metodoPago:{$regex:"^\\w+\\s\\w+$"}})
db.facturacion.find({$and:[{monto:{$gt:1600000}},{servicio:"Desarrollo Web"}]})
db.facturacion.find({$or:[{monto:{$lt:1500000}},{estoPago:"finalizado"}]})
db.facturacion.find({metodoPago:{$regex:"^e......o"}})
