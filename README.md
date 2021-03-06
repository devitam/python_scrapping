# Python scrapping

#### Pasos
1) Buscar zipcodes https://www.zipcodestogo.com/Maryland/ (copiar y pegar en Excel, después en Stata - líneas 3 a 11 del do file de Stata)

HECHO con código de python en vez de copiar y pegar de la página. Adjuntamos el código con comentarios (zipcodes.py).

2) Bajar datos de crimen de https://odn.data.socrata.com/dataset/National-Police-Department-Crime-Rates-by-Month-Ye/tt5s-y5fc (hecho en clase llamado crime.csv). Quedarse con los datos de 2015 y el estado MD, guardar como MD_crime.dta (líneas 14 a 22 del do file de Stata).

HECHO creamos una cuenta aquí.

3) Merge base zipcodes y crimen (necesito ubicar los zipcodes para bajar el weather después).

HECHO.

4) Bajar shapefile https://hub.arcgis.com/datasets/maryland::maryland-physical-boundaries-county-boundaries-detailed/explore?location=38.802591%2C-77.268250%2C8.35 y abrir con Excel el archivo .dbf para obtener el ID de cada county. Agregar el ID (sacado del shapefile) para después poder hacer el merge (líneas 31 a 55 Stata.).

HECHO.

5) linea 59 de Stata suma los crimenes por county, linea 61 me genera un zipcode por county (el zipcode mediano), línea 63 me quedo con una observación por county, por año, por mes, por tipo de crimen -> MD_crime_2015.dta.

HECHO.

6) en la línea 68 le pido a Stata los zipcodes para poner en python para que me baje los datos de weather (usar el Inicial.py) agregando los zips, corrigiendo año y frecuency *24*.

HECHO, Stata nos dio 24 zipcodes, más que en el video. Adjunto inicial.py donde está el código para descargar los datos de weather.

7) línea 71 a 92 genera nueva base para que cada columna sea un crimen.

HECHO.

8) línea 95 a 110 junta las bases de weather quedándose con el promedio de precipitaciones por mes (línea 104) y una observación por mes/county (linea 105).

HECHO.

9) Merge crimen,zipcodes+weather (línea 117).

HECHO.

#### Consignas

Gráficos a hacer:
1) Gráfico entre precipitaciones y algún crímen per cápita. Explicar.

Para esto, abrimos QGIS y subimos la base de Maryland Boundaries. Por otro lado, tomamos la base de MD_crime_2015_wide.dta y calculamos las precipitaciones promedio por año y sumamos los crímenes por año. Pegamos esa base agregada con la de Maryland Boundaries e hicimos los gráficos. El resultado se muestra en el archivo en pdf.

2) Usar la variable BLACK para generar algo (gráfico o mapa) interesante (potencialmente interesante, puede que con estos datos no de nada).

Usamos la misma base que en el inciso anterior y armamos un scatter plot. También en el archivo en pdf.

3) Mapa que avance en el tiempo por mes de precipitaciones y de uno de los crímenes per cápita (Properties > Temporal después de haber hecho un coropletico o heatmap. Ver: https://www.qgistutorials.com/en/docs/3/animating_time_series.html. Generar variable de date con función make_date y las variables, year, month y day. Ojo que ya existe la variable date y salta error si le ponen el mismo nombre). En heatmap, poner como transparente cuando es 0 la variable. 

Para hacer el merge de la base Maryland Boundaries y MD_crime_2015_wide, multiplicamos por doce a la primera y le subimos la segunda. Usando el agregador de campo que auto-incrementa agrupado por OBJECTID (en QGIS, Caja de Herramientas > Tabla vectorial > Agregar campo que auto-incrementa) y concatenando el resultado con ID, armamos una variable para hacer el merge. Hicimos lo mismo en MD_crime_2015_wide. Hicimos la unión y luego definimos una variable que contenía la fecha (date). Siguiendo los pasos en este [enlace](https://www.qgistutorials.com/en/docs/3/animating_time_series.html), creamos las dos imágenes en GIF.

Se entregan 3 archivos en GitHub (Poner link en la entrega de la tarea):

LaTeX con consignas 1 y 2

GIF con consigna 3.

Archivo .py (Inicial.py) para bajar lo de weather para los zipcodes correspondientes.
