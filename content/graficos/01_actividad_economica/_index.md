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

{{< bokeh 01.01_emae.json >}}

> * FUENTE:
>   * [Ministerio de Economía | Portal de Económicos: Actividad Económica](https://www.economia.gob.ar/datos/)
>   * Cálculos del autor.

---

## Gráfico 2. PBI real (1994 - 2019)

{{< bokeh 01.02_pbi_real.json >}}

> * FUENTE:
>   * [Instituto Nacional de Estadísticas y Censos (INDEC)](https://www.indec.gob.ar/indec/web/Nivel4-Tema-3-9-47)

---

## Gráfico 3. PBI real (1993) por sector: Valor agregado bruto a precios de productor

{{< bokeh 01.03_pbi_real_1993_sector.json >}}

> * FUENTE:
>   * [Ministerio de Economía | Portal de Datos Económicos: Actividad Económica](https://www.economia.gob.ar/datos/)
> ---
> **Nota metodológica**: Siendo `VA` valor agregado:  
> `PBI` =  `VA bruto` + `Impuesto al VA` + `Impuesto a las importacIones`  
> `VA bruto` = $\sum$ `VA por sector` - `Intermediación financiera medido indirectamente`

---

## Gráfico 4. PBI real (1993) participación por sector: Valor agregado bruto a precios de productor

{{< bokeh 01.04_pbi_real_1993_sector_part.json >}}

> * FUENTE:
>   * [Ministerio de Economía | Portal de Datos Económicos: Actividad Económica](https://www.economia.gob.ar/datos/)

---

## Gráfico 5. PBI real (2004) por sector: Valor agregado bruto a precios de productor

{{< bokeh 01.05_pbi_real_2004_sector.json >}}

> * FUENTE:
>   * [Ministerio de Economía | Portal de Datos Económicos: Actividad Económica](https://www.economia.gob.ar/datos/)
> ---
> **Nota metodológica**: Siendo `VA` valor agregado:  
> `PBI` =  `VA bruto` + `Impuesto al VA` + `Derechos a las importacIones` + `Impuestos netos de subsidios`
> `VA bruto` = $\sum$ `VA por sector`

---

## Gráfico 6. PBI real (2004) participación por sector: Valor agregado bruto a precios de productor

{{< bokeh 01.06_pbi_real_2004_sector_part.json >}}

> * FUENTE:
>   * [Ministerio de Economía | Portal de Datos Económicos: Actividad Económica](https://www.economia.gob.ar/datos/)

---

## Gráfico 7. Productividad total de los factores de producción en moneda local, Argentina (2017 = 1)

{{< bokeh 01.07_TFP_ARG.json >}}

> * FUENTE:
>   * [Penn World Table 10.0](https://www.rug.nl/ggdc/productivity/pwt/?lang=en)

---

## Gráfico 8. Productividad en países selectos (USA = 1)

{{< bokeh 01.08_TFP_Comparado.json >}}

> * FUENTE:
>   * [Penn World Table 10.0](https://www.rug.nl/ggdc/productivity/pwt/?lang=en)