# Documento de Requerimientos: Sistema de Gestión para Torneos Deportivos

# 1.Introducción:

+ El propósito de este sistema es gestionar la información relacionada con los participantes en un evento deportivo de torneos en Sudamérica. Se debe diseñar una base de datos MongoDB que contemple las siguientes colecciones: deportistas, equipos, entrenadores, árbitros, encuentros deportivos, resultados y posiciones.
Deportistas:
Cada deportista debe tener un identificador único, nombre, apellido, fecha de nacimiento, posición en el campo, equipo al que pertenece y estadísticas relevantes (goles marcados, tarjetas recibidas, etc.). Se debe garantizar que un deportista no pueda participar en más de un equipo durante el torneo.

# 2.Equipos:
+ Cada equipo debe tener un identificador único, nombre y detalles adicionales según sea necesario en el contexto del torneo (país, ciudad, etc.).

# 3.Entrenadores:
+ Cada entrenador debe tener un identificador único, nombre, apellido, fecha de nacimiento y equipo al que pertenece. No puede haber dos entrenadores con el mismo identificador.

# 4.Árbitros:
+ Cada árbitro debe tener un identificador único, nombre, apellido y estadísticas relevantes (número de partidos dirigidos, tarjetas mostradas, etc.). No puede haber dos árbitros con el mismo identificador.

# 5.Encuentros Deportivos:
+ Cada encuentro debe tener un identificador único, fecha y hora, lugar, equipos participantes y el identificador del árbitro designado. Debe registrarse el estado del encuentro (por ejemplo, programado, en curso, finalizado).

# 6.Resultados:
+ Cada resultado debe tener un identificador único, identificador del encuentro, goles marcados por cada equipo y cualquier evento relevante (tarjetas rojas, tarjetas amarillas, etc.). Los resultados solo pueden registrarse una vez que el encuentro esté finalizado.

# 7.Posiciones:
+ Debe calcularse y almacenarse la posición de cada equipo en la tabla de posiciones, considerando puntos, goles a favor, goles en contra y diferencia de goles. La tabla de posiciones debe ser actualizada automáticamente después de cada encuentro.

# 8.Reglamento del Torneo:
+ Cada encuentro se rige por las reglas estándar del deporte correspondiente. Se otorgan puntos según el resultado de cada encuentro. En caso de empate en puntos, se utiliza la diferencia de goles para determinar la posición en la tabla.
