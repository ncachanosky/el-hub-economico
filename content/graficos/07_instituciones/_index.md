---
# Title, summary, and page position.
linktitle: "Series institucionales"
weight: 7

# Page metadata.
title: Series institucionales
type: book  # Do not modify.
---

{{% callout note %}}
Página en desarrollo
{{% /callout %}}

---

## Gráfico 1. Ministros de Economía (días en ejercicio)

{{< bokeh ministros_dias.json >}}

> * FUENTES:
>   * Cálculos del autor

---

## Gráfico 2. Presidentes del BCRA (días en ejercicio)

{{< bokeh bcra_dias.json >}}

> * FUENTES:
>   * Cálculos del autor

---

## Gráfico 3. Índice de libertad económica

{{< bokeh efw_rank.json >}}

> * FUENTES:
>   * [Fraser Institute. *Economic Freedom of the World*](https://www.fraserinstitute.org/economic-freedom/map)

---

## Gráfico 4. Índice de libertad económica y PBI per cápita

{{< bokeh efw_gdp.json >}}

> * FUENTES:
>   * [Fraser Institute. *Economic Freedom of the World*](https://www.fraserinstitute.org/economic-freedom/map)
>   * [Banco Mundial: World Development Indicators](https://datatopics.worldbank.org/world-development-indicators/)

---

## Gráfico 5. Índice de libertad económica por región

{{< bokeh efw_regional.json >}}

> * FUENTES:
>   * [Fraser Institute. *Economic Freedom of the World*](https://www.fraserinstitute.org/economic-freedom/map)
>   * [Banco Mundial: World Development Indicators](https://datatopics.worldbank.org/world-development-indicators/)
>   * Cálculos del autor
> ---
> **Nota metodológica**: Los índices regionales son promedios ponderados por población

---

## Gráfico 6. Índice de libertad económica y participación del ingeso del primer decil

{{< bokeh efw_bottom_10.json >}}

> * FUENTES:
>   * [Fraser Institute. *Economic Freedom of the World*](https://www.fraserinstitute.org/economic-freedom/map)
>   * [Banco Mundial: World Development Indicators](https://datatopics.worldbank.org/world-development-indicators/)
>   * Cálculos del autor
> ---
> **Nota metodológica**: Promedio de la participación del ingreso del primer decil por país (no ponderado por población) por cuartil de libertad económica.

---

## Gráfico 7. Índice de libertad económica y índice de GINI

{{< bokeh efw_GINI.json >}}

> * FUENTES:
>   * [Fraser Institute. *Economic Freedom of the World*](https://www.fraserinstitute.org/economic-freedom/map)
>   * [Banco Mundial: World Development Indicators](https://datatopics.worldbank.org/world-development-indicators/)
>   * Cálculos del autor
> ---
> **Nota metodológica**: Promedio del índice de GINI por país (no ponderado por población) por cuartil de libertad económica.
> $\text{(mayor igualdad) }0 \leftarrow GINI \rightarrow 100 \text{ (mayor desigualdad)}$