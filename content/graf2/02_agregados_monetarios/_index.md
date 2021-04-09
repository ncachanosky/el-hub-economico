---
# Title, summary, and page position.
linktitle: "Agregdos monetarios y precios"
weight: 2

# Page metadata.
title: Agregdos monetarios y precios
type: book  # Do not modify.
---

---

## Gráfico 1: Inflación interanual

{{< bokeh inflacion_interanual.json >}}

> * FUENTES:
>   * [Instituto Nacional de Estadsticas y Censos (INDEC)](https://www.indec.gob.ar/indec/web/Nivel4-Tema-3-9-47)
>   * Los datos del **IPC Congreso** fueron recolectados de manera manual por el autor

---

## Gráfico 2: Agregados monetarios e IPC

{{< bokeh agregados_monetarios_ipc.json >}}

> * FUENTE:
>   * [Instituto Nacional de Estadsticas y Censos (INDEC)](https://www.indec.gob.ar/indec/web/Nivel4-Tema-3-9-47)
>   * IPC Congreso
>   * Cálculos del autor
> ---
> **Nota metodológica**: La serie IPC fue corregida con datos de la "Inflación Congreso" para el período enero 2007 - diciembre 2015.

---

## Gráfico 3: Tiempo en que se duplica el nivel de precios

{{< bokeh precios_x2.json >}}

> * FUENTE:
>   * [Instituto Nacional de Estadsticas y Censos (INDEC)](https://www.indec.gob.ar/indec/web/Nivel4-Tema-3-9-47)
>   * IPC Congreso
>   * Cálculos del autor
> ---
> **Nota metodológica**: La serie IPC fue corregida con datos de la "Inflación Congreso" para el período enero 2007 - diciembre 2015. La serie estima el tiempo que tarda en duplicarse el nivel de precios con la tasa de inflación interanual de cada período.