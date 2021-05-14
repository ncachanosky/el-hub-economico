[![Netlify Status](https://api.netlify.com/api/v1/badges/81e3b877-3a74-40a1-a5f4-2b1d493ea930/deploy-status)](https://app.netlify.com/sites/elhubeconomico/deploys)

# El Hub Económico

Sitio web: https://www.elhubeconomico.com/

---

Encontrar fuentes de datos económicos de Argentina no siempre es fácil. **El Hub Económico** recopila fuentes de libre acceso y ofrece una selección de gráficas dela economía del país así como de Argentina en el mundo.

Los gráficos se agrupan en las siguientes categorías: 

1. Actividad económica
2. Agregados monetarios y precios
3. Mercado laboral y pobreza
4. Datos fiscales
5. Desarrollo y series de largo plazo
6. Series institucionales

Las fuentes de datos se agrupan de la siguientes manera:

1. Fuentes oficiales
2. Fuentes privadas
3. Fuentes internacionales

## Cómo contribuir

* Abrir un [issue](https://github.com/ncachanosky/el-hub-economico/issues) con:
  * Errores u omisiones
  * Nuevas fuentes de datos a incluir
  * Nuevos gráficos
* Sponsorear](https://github.com/sponsors/ncachanosky) el proyecto

## ¿Cómo se construye el Hub Económico?

### Sitio web

El sitio web está construido con [Wowchemy](https://wowchemy.com/) for [Hugo](https://gohugo.io/).
El "deploy" del sitio es a través de [Netlify](https://www.netlify.com/).

### Gráficos
Los gráficos interactivos se construyen con [Bokeh](https://bokeh.org/)
Los códigos Python de los gráficos están escritos en [Jupyter Notebooks](https://jupyter.org/) y se pueden consultar en: `static/Jupyter Notebooks/`.