# 🌧️ Automatización de registros de precipitaciones rurales – Chivilcoy

**Prototipo de aplicación de inteligencia artificial para interpretar, organizar y validar reportes de precipitaciones rurales.**

Proyecto final de la Diplomatura en Inteligencia Artificial – Facultad de Ciencias Económicas, Universidad de Buenos Aires (FCE-UBA).

## 1. Problema que buscamos resolver

La Agencia de Extensión Rural (AER) Chivilcoy del Instituto Nacional de Tecnología Agropecuaria (INTA) recibe información de precipitaciones de distintos puntos del partido de Chivilcoy.

Los informantes comunican las lluvias principalmente mediante mensajes de WhatsApp, utilizando expresiones informales y formatos diferentes.

Actualmente, el procesamiento requiere tareas manuales: interpretar mensajes, identificar localidades, distinguir nuevos registros de correcciones, calcular acumulados y organizar la información para su posterior análisis y comunicación.

Este procedimiento demanda tiempo y puede generar dificultades cuando existen mensajes incompletos, registros adicionales o correcciones posteriores.

## 2. Objetivo del proyecto

Desarrollar un prototipo que permita automatizar parcialmente el procesamiento de los reportes de precipitaciones, incorporando inteligencia artificial para interpretar mensajes escritos en lenguaje natural.

La solución busca reducir tareas repetitivas, mejorar la trazabilidad de los datos y facilitar su revisión, manteniendo la validación humana como instancia necesaria antes de utilizar la información como definitiva.

## 3. Tecnologías utilizadas

- **n8n:** automatización y coordinación del flujo de trabajo.
- **Google Gemini:** interpretación de mensajes mediante inteligencia artificial generativa.
- **Google Sheets:** almacenamiento de informantes, eventos, registros y acumulados.
- **JavaScript:** normalización de datos, identificación de mensajes y control de duplicados.
- **GitHub:** documentación y presentación del prototipo.

## 4. Funcionamiento del prototipo

El flujo desarrollado realiza las siguientes operaciones:

1. Recibe un mensaje de prueba ingresado manualmente.
2. Envía su contenido a Gemini para interpretar la cantidad de lluvia y el tipo de registro.
3. Identifica al informante mediante un número de teléfono ficticio incluido en el mensaje de prueba.
4. Consulta la base de informantes y determina el punto de medición correspondiente.
5. Identifica el evento de precipitación abierto.
6. Genera un identificador del mensaje para evitar registros duplicados.
7. Guarda el registro en Google Sheets.
8. Permite calcular acumulados y visualizar estados de revisión.

**El prototipo no se conecta automáticamente a WhatsApp.** Actualmente se utilizan mensajes ingresados manualmente para simular el proceso de recepción.

## 5. Tipos de mensajes interpretados

Se contemplan las siguientes categorías:

- **TOTAL:** cantidad informada como total de precipitación.
- **ADICIONAL:** lluvia agregada a una medición anterior.
- **CORRECCION:** modificación de un valor previamente informado.
- **AMBIGUO:** mensaje que no permite determinar con suficiente claridad su significado.

Un valor explícito de **0 mm** se considera válido y se diferencia de un dato faltante.

## 6. Pruebas realizadas

Se realizaron pruebas con mensajes ficticios correspondientes al punto de medición Gorostiaga (P05).

**Evento EV-PRUEBA-001**

Se verificó el registro de una medición inicial, un adicional, una corrección y un nuevo adicional posterior.

El cálculo probado permitió obtener 22 mm a partir de una corrección a 18 mm y 4 mm adicionales posteriores.

También se comprobó el registro de un mensaje que informaba 0 mm.

**Evento EV-PRUEBA-002**

Se realizaron pruebas con una medición inicial de 10 mm, un adicional de 5 mm, dos correcciones sucesivas a 17 y 19 mm, y un adicional posterior de 2 mm.

El cálculo final probado fue de **21 mm**.

Asimismo, se verificó la identificación del evento abierto y el control de mensajes duplicados.

Estas pruebas corresponden a escenarios específicos y no constituyen una validación exhaustiva del sistema.

## 7. Validación humana

La solución está diseñada como una herramienta de apoyo, no como un sistema que aprueba automáticamente los datos.

Google Sheets permite distinguir registros pendientes de validación y acumulados que necesitan una nueva revisión cuando cambia el valor previamente aprobado.

La decisión final sobre la aceptación de los datos permanece bajo responsabilidad humana.

## 8. Limitaciones actuales

El prototipo presenta limitaciones que deberán abordarse en futuras etapas:

- No existe todavía una integración automática con WhatsApp.
- La identificación del informante depende del formato utilizado en los mensajes de prueba.
- La clasificación de mensajes mediante IA puede cometer errores.
- Los cálculos de acumulados se probaron en escenarios determinados, pero no se validaron todas las combinaciones posibles de mensajes `TOTAL`, correcciones y registros fuera de orden.
- La aprobación humana todavía se representa mediante campos de Google Sheets y no mediante una interfaz específica.
- La generación automática de mapas e informes finales no forma parte del flujo de n8n actualmente implementado.

## 9. Próximos desarrollos

Se propone continuar con la ampliación de las pruebas, el tratamiento de mensajes ambiguos, la mejora de la identificación de informantes, la automatización de los controles de revisión y la generación de productos de comunicación, como tablas, mapas e informes de precipitaciones.

## 10. Alcance

Este proyecto es un **prototipo académico y experimental**. Utiliza datos de prueba y no reemplaza los procedimientos oficiales de registro, validación y publicación de información del INTA.

Su propósito es demostrar cómo la inteligencia artificial generativa, combinada con herramientas de automatización, puede contribuir a mejorar procesos de trabajo existentes.
