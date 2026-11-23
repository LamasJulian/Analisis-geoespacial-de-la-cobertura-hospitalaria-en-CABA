# Análisis geoespacial de la cobertura hospitalaria en CABA

¿La oferta de hospitales de la Ciudad Autónoma de Buenos Aires acompaña a la población de cada comuna? Este proyecto cruza la ubicación de los hospitales públicos, la población por comuna y los límites territoriales para medir **cuántos hospitales hay** y, sobre todo, **qué tan cerca están** los vecinos de uno.

El análisis completo está en [`cobertura_hospitalaria_caba.ipynb`](cobertura_hospitalaria_caba.ipynb).

## Hallazgos principales

- **La oferta está concentrada.** La Comuna 4 reúne 13 de los 36 hospitales (36%) con el 7,8% de la población, mientras que la Comuna 1, la más poblada, no tiene ninguno.
- **El tipo de hospital cambia el diagnóstico.** Solo 14 de los 36 son hospitales generales de agudos (los que atienden urgencias de cualquier vecino). Con ese filtro la Comuna 4 pasa de 13 a 2 hospitales, y las comunas 1, 5 y 13 quedan sin ninguno dentro de sus límites.
- **Contar hospitales por comuna no alcanza.** Con un radio de 2,5 km (unos 30 minutos a pie) alrededor de cada hospital de agudos se cubre el 84,0% de la superficie de CABA. La Comuna 5 no tiene hospital propio pero queda cubierta al 100% por los de comunas vecinas.
- **Las comunas con menor cobertura** son la 13 (53,2%), la 1 (66,5%), la 14 (67,0%), la 12 (74,1%) y la 8 (74,6%). Suponiendo población uniforme dentro de cada comuna, unas 440.000 personas (14,3%) viven a más de 2,5 km de un hospital general de agudos.

## Qué hace el notebook

1. Exploración y limpieza de tres datasets: hospitales, población por comuna y comunas (polígonos).
2. Preprocesamiento espacial: reproyección a un sistema de coordenadas en metros (EPSG:5347) y tratamiento de valores faltantes.
3. Indicadores de cobertura por comuna: hospitales cada 100.000 habitantes y por km².
4. Análisis de accesibilidad con búferes de distancia alrededor de cada hospital de agudos, con sensibilidad del radio (1 a 10 km).
5. Mapas estáticos e interactivos (Folium) y conclusiones.

## Cómo ejecutarlo

```bash
pip install -r requirements.txt
jupyter notebook cobertura_hospitalaria_caba.ipynb
```

Los datos están en la carpeta `datos/` y el notebook los lee con rutas relativas, por lo que hay que abrirlo desde la raíz del repositorio. También funciona en Google Colab subiendo la carpeta `datos/` al panel de archivos. Los mapas interactivos cargan el mapa base desde internet.

## Datos

| Archivo | Contenido |
|---|---|
| `datos/hospitales.xlsx` | Hospitales públicos de CABA (36 registros, con ubicación). |
| `datos/comunas.csv` | Las 15 comunas con barrios, perímetro, área y geometría. |
| `datos/PDE.xlsx` | Población, superficie y densidad por comuna (año 2024). |

Fuentes: datos abiertos de la Ciudad Autónoma de Buenos Aires (hospitales y comunas) y Instituto de Estadística y Censos de la Ciudad (población).

## Limitaciones

- El dataset de hospitales no incluye clínicas ni sanatorios privados, por lo que la cobertura real podría ser mayor.
- Se asumió población uniforme dentro de cada comuna; datos por radio censal darían una estimación más precisa.
- Las distancias son en línea recta, sin considerar calles ni transporte.
- No se evaluó la capacidad de los hospitales (camas, guardias, complejidad).
- La superficie de las comunas difiere levemente entre la planilla oficial y la calculada desde los polígonos (205,9 vs. 204,4 km² en total).

## Autoría

Proyecto realizado en equipo. Mi aporte principal fue el análisis de accesibilidad con búferes de 2,5 km: la sensibilidad del radio, la cobertura por comuna, la estimación de población sin cobertura y los mapas correspondientes.

Julián Lamas · [GitHub](https://github.com/LamasJulian)
