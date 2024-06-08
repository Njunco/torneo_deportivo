
# Documento de Casos de Prueba para Validar el Particionamiento
Introducción
Este documento establece los casos de prueba para verificar la correcta implementación del mecanismo de particionamiento (sharding) en el Sistema de Gestión para Torneos de Fútbol. Los casos de prueba se centran en garantizar que el sistema cumple con los requerimientos no funcionales de redundancia y disponibilidad 24x7.

# Casos de Prueba
Verificación de la Configuración Inicial del Sharding

+ Caso de Prueba 1: Estado de los Servidores de Configuración

+ Objetivo: Verificar que los servidores de configuración estén funcionando correctamente.
+ Pasos:
1. Conectar al servidor de configuración principal.
2. Ejecutar el comando rs.status() para verificar el estado del conjunto de replicación.
+ Resultado Esperado: Todos los servidores de configuración deben estar en estado "PRIMARY" o "SECONDARY".
# Caso de Prueba 2: Estado de los Shards

+ Objetivo: Verificar que los servidores de shard estén funcionando correctamente.
+ Pasos:
1. Conectar a cada servidor de shard.
2. Ejecutar el comando rs.status() para verificar el estado del conjunto de replicación.
+ Resultado Esperado: Todos los servidores de shard deben estar en estado "PRIMARY" o "SECONDARY".
  
2. Verificación de la Funcionalidad del Sharding

# Caso de Prueba 3: Agregar y Consultar Datos en una Colección Shardeada

+ Objetivo: Verificar que se pueden agregar y consultar datos en una colección shardeada.
+ Pasos:
1. Conectar al router mongos.
2. Insertar un documento en la colección deportistas.
3. Consultar el documento insertado.
+ Resultado Esperado: El documento debe ser insertado y recuperado correctamente.
# Caso de Prueba 4: Balanceo de Carga

+ Objetivo: Verificar que el balanceo de carga funciona correctamente.
+ Pasos:
1. Insertar múltiples documentos en la colección encuentros_deportivos.
2. Verificar la distribución de los datos entre los shards.
+ Resultado Esperado: Los datos deben estar distribuidos equitativamente entre los shards.
3. Verificación de la Redundancia y Disponibilidad

# Caso de Prueba 5: Failover de Shards

+ Objetivo: Verificar que el sistema puede manejar fallos en un shard.
+ Pasos:
1. Apagar un nodo del shard primario.
2. Verificar que otro nodo asuma el rol de primario.
+ Resultado Esperado: Otro nodo debe asumir el rol de primario sin pérdida de datos.
+ Caso de Prueba 6: Failover de Config Servers

+ Objetivo: Verificar que el sistema puede manejar fallos en un servidor de configuración.
+ Pasos:
Apagar un servidor de configuración.
Verificar que el sistema sigue funcionando correctamente.
Resultado Esperado: El sistema debe seguir funcionando sin interrupciones.

# Ejecución de los Casos de Prueba
1. Estado de los Servidores de Configuración

```
mongo --port 27019
rs.status()
```
2. Estado de los Shards

```
mongo --port 27001
rs.status()
```
```
mongo --port 27002
rs.status()
```
3. Agregar y Consultar Datos en una Colección Shardeada
```
mongo --host localhost --port 27017

db.deportistas.insert({
  _id: 3,
  nombre: "Luis",
  apellido: "Suarez",
  fecha_nacimiento: ISODate("1987-01-24T00:00:00Z"),
  posicion: "Delantero",
  equipo: "uru",
  goles: 4,
  tarjetas_amarillas: 1,
  tarjetas_rojas: 0
})

db.deportistas.find({ nombre: "Luis" })
```
4. Balanceo de Carga
```

for (let i = 1; i <= 1000; i++) {
  db.encuentros_deportivos.insert({
    _id: i,
    fecha_hora: new Date(),
    lugar: "Estadio",
    equipos: ["teamA", "teamB"],
    arbitro: i % 5,
    estado: "Programado"
  })
}

db.stats()
```

5. Failover de Shards
```
mongo --port 27001
rs.stepDown()
```
Verificar el estado del conjunto de replicación.
```
rs.status()
```
6. Failover de Config Servers
+ Apagar un servidor de configuración y verificar el estado.
```
mongo --port 27019
rs.status()
```

# Reporte de Resultados y Análisis
Caso de Prueba 1: Estado de los Servidores de Configuración

+ Resultado: Todos los servidores de configuración están en estado "PRIMARY" o "SECONDARY".
+ Análisis: La configuración inicial de los servidores de configuración es correcta.
  
Caso de Prueba 2: Estado de los Shards

+ Resultado: Todos los servidores de shard están en estado "PRIMARY" o "SECONDARY".
+ Análisis: La configuración inicial de los shards es correcta.
  
Caso de Prueba 3: Agregar y Consultar Datos en una Colección Shardeada

+ Resultado: El documento se inserta y recupera correctamente.
+ Análisis: La funcionalidad básica de sharding está funcionando correctamente.
  
Caso de Prueba 4: Balanceo de Carga

+ Resultado: Los datos están distribuidos equitativamente entre los shards.
+ Análisis: El balanceo de carga está funcionando correctamente.
  
Caso de Prueba 5: Failover de Shards

+ Resultado: Otro nodo asume el rol de primario sin pérdida de datos.
+ Análisis: El sistema maneja correctamente el failover de shards.
  
Caso de Prueba 6: Failover de Config Servers

+ Resultado: El sistema sigue funcionando sin interrupciones.
+ Análisis: El sistema maneja correctamente el failover de servidores de configuración.


