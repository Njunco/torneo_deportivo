
# los servidores de shard deben estar en estado "PRIMARY" o "SECONDARY".
# Verificación de la Funcionalidad del Sharding

# Caso de Prueba 3: Agregar y Consultar Datos en una Colección Shardeada

# Objetivo: Verificar que se pueden agregar y consultar datos en una colección shardeada.
Pasos:
+ Conectar al router mongos.
+ Insertar un documento en la colección deportistas.
+ Consultar el documento insertado.
# Resultado Esperado: El documento debe ser insertado y recuperado correctamente.
Caso de Prueba 4: Balanceo de Carga

# Objetivo: Verificar que el balanceo de carga funciona correctamente.
Pasos:
+ Insertar múltiples documentos en la colección encuentros_deportivos.
+ Verificar la distribución de los datos entre los shards.
# Resultado Esperado: Los datos deben estar distribuidos equitativamente entre los shards.
Verificación de la Redundancia y Disponibilidad

# Caso de Prueba 5: Failover de Shards

# Objetivo: Verificar que el sistema puede manejar fallos en un shard.
Pasos:
+ Apagar un nodo del shard primario.
+ Verificar que otro nodo asuma el rol de primario.
# Resultado Esperado: Otro nodo debe asumir el rol de primario sin pérdida de datos.
# Caso de Prueba 6: Failover de Config Servers

# Objetivo: Verificar que el sistema puede manejar fallos en un servidor de configuración.
Pasos:
+ Apagar un servidor de configuración.
+ Verificar que el sistema sigue funcionando correctamente.
# Resultado Esperado: El sistema debe seguir funcionando sin interrupciones.
