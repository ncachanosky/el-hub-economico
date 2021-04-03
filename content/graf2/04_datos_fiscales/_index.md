---
# Title, summary, and page position.
linktitle: "Datos fiscales"
weight: 5

# Page metadata.
title: Datos fiscales
type: book  # Do not modify.
---

{{< toc >}}

---

## Gráfico 1: Déficiti fiscal (nación y consolidado) (1961 - 2019)

{{< bokeh fiscal_deficit.json >}}

> * FUENTES: 
>   * Ministerio de Economía | [Oficina Nacional de Presupuesto](https://www.economia.gob.ar/onp/documentos/series/Serie1961-2004.pdf) 
>   * Ministerio de Economía | [Boletín Fiscal](https://www.economia.gob.ar/onp/ejecucion/2020)
>   * Cálculos del autor
> ---
> **Nota metodológica**: Al resultado financiero oficial se le substraen las transferencias de ANSES y BCRA que, bajo período 2003 - 2017 se contabilizaban como ingresos "regulares" del Tesoro Nacional. Por consistencia se substrean los mismos montos para los años anteriores al 2003 (montos sin impacto substancial en el resultado fiscal del Tesoro). El resultado fiscal también substrae los intereses intra sector público

---

## Gráfico 2: Gasto del tesoro nacional (pesos del 2002 | 2002 = 100)

{{< bokeh gasto_tesoro_100.json >}}

> * FUENTES: 
>   * Ministerio de Economía | [Boletín Fiscal](https://www.economia.gob.ar/onp/ejecucion/2020)
>   * Cálculos del autor
> 
---

## Gráfico 3: Deuda de la administración central

{{< bokeh deuda_publica.json >}}

> * FUENTE 
>   * Ministerio de Economía | [Secretaría de Finanzas](https://www.argentina.gob.ar/economia/finanzas/presentaciongraficadeudapublica)

---

## Gráfico 4: Gasto consolidado por nivel de gobierno (1980 - 2017)

{{< bokeh gasto_consolidado_nivel.json >}}

> * FUENTE 
>   * Ministerio de Economía | [Secretaría de Política Económica](https://www.argentina.gob.ar/economia/politicaeconomica/macroeconomica/gastopublicoconsolidado)