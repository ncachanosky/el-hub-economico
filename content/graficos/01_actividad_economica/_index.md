---
# Title, summary, and page position.
linktitle: "Actividad económica"
weight: 2

# Page metadata.
title: Actividad económica
date: "2018-09-09T00:00:00Z"
type: book  # Do not modify.
---

---

{{% callout note %}}
Página en desarrollo
{{% /callout %}}

---

## Gráfico 1. Estimador Mensual de Actividad Económica (EMAE)

{{< bokeh emae.json >}}

<a href="https://twitter.com/share?ref_src=twsrc%5Etfw" class="twitter-share-button" data-text="Estimador Mensual de Actividad Económica (EMAE)" data-url="https://www.elhubeconomico.com/graficos/01_actividad_economica/#gr%C3%A1fico-1-estimador-mensual-de-actividad-econ%C3%B3mica-emae" data-via="n_cachanosky" data-show-count="false">Tweet</a><script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

> * FUENTE:
>   * [Ministerio de Economía | Datos Económicos: Actividad Económica](https://www.economia.gob.ar/datos/)
>   * Cálculos del autor.

## Gráfico 2. PBI real (1994 - 2019)

{{< bokeh pbi_real.json >}}

> * FUENTE:
>   * [Instituto Nacional de Estadísticas y Censos (INDEC)](https://www.indec.gob.ar/indec/web/Nivel4-Tema-3-9-47)

---

## Gráfico 3. PBI real (1993) por sector: Valor agregado bruto a precios de productor

{{< bokeh pbi_real_1993_sector.json >}}

> * FUENTE:
>   * [Ministerio de Economía | Datos Económicos: Actividad Económica](https://www.economia.gob.ar/datos/)
> ---
> **Nota metodológica**: Siendo `VA` valor agregado:  
> `PBI` =  `VA bruto` + `Impuesto al VA` + `Impuesto a las importacIones`  
> `VA bruto` = $\sum$ `VA por sector` - `Intermediación financiera medido indirectamente`

---

## Gráfico 4. PBI real (1993) participación por sector: Valor agregado bruto a precios de productor

{{< bokeh pbi_real_1993_sector_part.json >}}

> * FUENTE:
>   * [Ministerio de Economía | Datos Económicos: Actividad Económica](https://www.economia.gob.ar/datos/)

---

## Gráfico 5. PBI real (2004) por sector: Valor agregado bruto a precios de productor

{{< bokeh pbi_real_2004_sector.json >}}

> * FUENTE:
>   * [Ministerio de Economía | Datos Económicos: Actividad Económica](https://www.economia.gob.ar/datos/)
> ---
> **Nota metodológica**: Siendo `VA` valor agregado:  
> `PBI` =  `VA bruto` + `Impuesto al VA` + `Derechos a las importacIones` + `Impuestos netos de subsidios`
> `VA bruto` = $\sum$ `VA por sector`

---

## Gráfico 6. PBI real (2004) participación por sector: Valor agregado bruto a precios de productor

{{< bokeh pbi_real_2004_sector_part.json >}}

> * FUENTE:
>   * [Ministerio de Economía | Datos Económicos: Actividad Económica](https://www.economia.gob.ar/datos/)