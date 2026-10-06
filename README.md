# Healthspan

Tablero de biomarcadores para seguir la salud de un grupo pequeño de personas a lo largo del tiempo. Cada participante tiene uno o más paneles de laboratorio ordenados por fecha; el tablero muestra cada valor frente al rango del laboratorio que lo emitió, el cambio frente al panel anterior, el contexto de la toma (ayuno, ejercicio, hora) y una lectura en lenguaje llano de lo que pesa y lo que no.

**Los participantes están anonimizados.** Se identifican como Participante A, B, … Se conservan edad, sexo y antecedentes familiares porque son necesarios para interpretar los valores.

## Qué contiene

- `DATA.md` — copia legible de todos los datos (paneles, valores, rangos, lecturas, próximo panel). Se regenera desde `index.html`.
- `index.html` — el tablero completo, autocontenido (HTML + CSS + JS, sin dependencias ni build). Los datos viven en el objeto `DATA` al final del archivo.

## Estructura de `DATA`

```
members[]          un participante
  id, name         identificador anónimo
  panels[]         un informe de laboratorio
    date, age, lab
    ranges         rangos del laboratorio cuando difieren de los genéricos de MARKERS
    results        { marcador: valor }
    notes[]        lecturas por hallazgo, con tono (ok / h = alto / l = bajo)
    context[]      condiciones de la toma
  followup[]       qué medir la próxima vez y cómo
```

Los marcadores y sus rangos genéricos están en `MARKERS`, agrupados por sistema (lípidos, metabolismo, hígado, riñón, hierro, hormonas, tiroides, micronutrientes, inflamación, sangre, próstata).

## Secciones del tablero

1. **Panel por fecha** — cada marcador con gauge, valor, rango y delta frente al panel anterior.
2. **Lecturas** — qué significa cada hallazgo relevante, qué parte puede deberse a las condiciones de la toma y qué conviene llevar a la consulta.
3. **Evolución** — sparklines por marcador para todo lo medido dos o más veces.
4. **Próximo panel** — qué repetir, cuándo y en qué condiciones.

## Reglas

- No diagnostica, no recomienda dosis, no reemplaza la consulta médica.
- Los rangos son los del laboratorio que emitió cada informe; cuando dos laboratorios difieren, manda el que emitió el resultado.
- Un valor fuera de rango se lee junto con las condiciones de la toma antes de darle peso.

## Deploy

Sitio estático. Push a `main` despliega en Vercel.
