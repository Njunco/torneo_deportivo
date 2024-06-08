
# Documento de Requerimientos No Funcionales y Estrategia de Particionamiento
# 1. Introducción
+ Este documento establece los requerimientos no funcionales y la estrategia de particionamiento (sharding) para el Sistema de Gestión para Torneos de Fútbol en Sudamérica, garantizando redundancia y disponibilidad 24x7.

# 2. Escenario de Particionamiento (Sharding)
+ El particionamiento o sharding es necesario en el escenario donde el sistema debe manejar una gran cantidad de datos relacionados con los deportistas, equipos, encuentros deportivos y resultados. Debido a la alta concurrencia y volumen de datos esperados durante el torneo, es crucial distribuir la carga entre varios nodos para garantizar:

# Alta disponibilidad y continuidad del servicio.
+ Redundancia y recuperación ante desastres.
+ Mejora en la capacidad de respuesta y distribución de carga.
# 3. Requerimientos No Funcionales
# 3.1 Redundancia
+ Descripción:
+ El sistema debe configurarse con redundancia para asegurar la continuidad del servicio.

# Criterios de Calidad:

+ Alta Disponibilidad: Mantener una disponibilidad del 99.9% o superior.
+ Replicación de Datos: Implementar replicación de datos en al menos tres nodos distribuidos geográficamente.
+ Balanceo de Carga: Distribuir eficientemente las solicitudes entre los servidores.
+ Monitorización Continua: Identificar y abordar proactivamente cualquier punto único de fallo.
+ 3.2 Disponibilidad 24x7
Descripción:
El sistema debe estar disponible las 24 horas del día, los 7 días de la semana.

# Criterios de Calidad:

+ Mantenimiento Programado: Minimizar las ventanas de mantenimiento, programándolas durante horas de baja actividad.
+ Respaldo Automático: Realizar respaldos automáticos de la base de datos al menos una vez al día.
+ Detección y Recuperación Automática: Equipar el sistema con mecanismos de detección y recuperación automática de fallos.
# 4. Estrategia de Particionamiento Horizontal (Sharding)
+ Definición de la Estrategia de Particionamiento:
+ La estrategia de particionamiento se basará en la clave equipo para distribuir uniformemente los datos. Este enfoque se elige para balancear la carga y mejorar el rendimiento de consultas específicas sobre equipos.

# Pasos para Configurar el Sharding:

# 4.1 Configurar los Servidores de Configuración (Config Servers)

+ 1.Iniciar los servidores de configuración:
```
mongod --configsvr --replSet rsConfig --dbpath /data/configdb1 --port 27019
mongod --configsvr --replSet rsConfig --dbpath /data/configdb2 --port 27020
mongod --configsvr --replSet rsConfig --dbpath /data/configdb3 --port 27021
```
+ 2.Inicializar el conjunto de replicación para los servidores de configuración:
```
mongo --port 27019

rs.initiate(
  {
    _id: "rsConfig",
    configsvr: true,
    members: [
      { _id: 0, host: "localhost:27019" },
      { _id: 1, host: "localhost:27020" },
      { _id: 2, host: "localhost:27021" }
    ]
  }
)
```
# 4.2 Configurar los Servidores de Shard

+ 1.Iniciar los servidores de shard:
```
mongod --shardsvr --replSet shard1 --dbpath /data/shard1 --port 27001
mongod --shardsvr --replSet shard2 --dbpath /data/shard2 --port 27002
mongod --shardsvr --replSet shard3 --dbpath /data/shard3 --port 27003
```

+ 2.Inicializar los conjuntos de replicación para cada shard:
```
mongo --port 27001

rs.initiate(
  {
    _id: "shard1",
    members: [
      { _id: 0, host: "localhost:27001" }
    ]
  }
)

mongo --port 27002

rs.initiate(
  {
    _id: "shard2",
    members: [
      { _id: 0, host: "localhost:27002" }
    ]
  }
)

mongo --port 27003

rs.initiate(
  {
    _id: "shard3",
    members: [
      { _id: 0, host: "localhost:27003" }
    ]
  }
)
```


