# Colaboracion entre agentes

Mantiene a tu equipo de soporte sincronizado con indicadores de presencia en tiempo real y notas internas fijadas. Sin necesidad de herramientas externas.

## Deteccion de colisiones

Cuando multiples agentes abren el mismo ticket, cada agente ve un indicador de avatar que muestra quien mas esta viendo actualmente. Esto previene respuestas duplicadas y esfuerzo desperdiciado.

- Pila de avatares con iniciales de otros observadores
- Tooltip "Tambien viendo" al pasar el cursor
- Se actualiza cada 30 segundos -- ligero, basado en cache (no requiere tabla de base de datos)

## Indicadores de escritura

Los agentes pueden transmitir el estado de escritura activa mientras redactan respuestas para que los companeros puedan evitar respuestas superpuestas.

- Estado de escritura en tiempo real por ticket
- Complementa la deteccion de colisiones para transferencias mas rapidas

## Notas internas fijadas

Las notas internas importantes se pueden fijar en la parte superior de la vista de detalle del ticket. Las notas fijadas se resaltan en una tarjeta de color ambar sobre el hilo de conversacion, para que los agentes no pasen por alto contexto critico.

- Fijar o desfijar cualquier nota interna con un solo clic
- Las notas fijadas se muestran en la parte superior del ticket, siempre visibles
- Solo las notas internas se pueden fijar -- las respuestas publicas no

## Panel de conocimiento

La barra lateral del ticket incluye un panel de conocimiento contextual para que los agentes puedan consultar contenido de ayuda relacionado sin salir de la vista del ticket.
