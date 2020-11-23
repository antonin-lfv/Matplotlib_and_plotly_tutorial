# Plotly and Matplotlib.pyplot tutorial
<br/>
<a href="https://www.python.org" class="fancybox" ><img align="right" width="110" height="110" src="https://user-images.githubusercontent.com/63207451/97306728-26fce600-185f-11eb-9784-14151a6b2c43.png"><a/>
	
## Introduction

Ce projet à pour objectif de présenter les modules __Matplotlib.pyplot__ et __Plotly__ qui sont les modules les plus utilisés pour faire de la visualisation de données avec Python. Plotly étant le plus compliqué mais également le plus interactif. Dans ce __README__ toutes les fonctions seront accompagnées du résultat. Le code complet pour ce repository est dans les fichiers sous le nom __code.py__ .
<br/>

## Index
- [Plotly](#Plotly)
	- [Importations](#importations)
	- [Première approche](#première-approche)
		- [Premier exemple](#premier-exemple)
		- [Deuxième exemple](#deuxième-exemple)
	- [Fonctions principales plotly.express](#fonctions-principales-plotlyexpress)
		- [Scatter plot](#scatter-plot)
		- [Courbe de tendance et densité](#courbe-de-tendance-et-densité)
		- [Error bars](#error-bars)
		- [Bar charts](#bar-charts)
		- [Graphiques de corrélations](#graphiques-de-corrélations)
		- [Scatter plot avec échelle des tailles des points](#scatter-plot-avec-échelle-des-tailles-des-points)
		- [Plot avec animation](#plot-avec-animation)
		- [Line Charts](#line-charts)
		- [Area charts](#area-charts)
		- [Pie charts](#pie-charts)
		- [Pie charts avec partie en dehors](#pie-charts-avec-partie-en-dehors)
		- [Donut charts](#donut-charts)
		- [Sunburst charts](#sunburst-charts)
		- [Treemaps](#treemaps)
		- [Histograms](#histograms)
		- [Boxplots](#boxplots)
		- [Violon plots](#violon-plots)
		- [Density contours](#density-contours)
		- [Heatmap](#heatmap)
		- [Point sur une carte](#point-sur-une-carte)
		- [Surface sur une carte](#surface-sur-une-carte)
		- [Polar plots](#polar-plots)
		- [Polar bar charts](#polar-bar-charts)
		- [Radar charts](#radar-charts)
		- [Coordonnées en 3D](#coordonnées-en-3d)
		- [Ternary charts](#ternary-charts)
	- [Graphiques multiples - Subplots](#graphiques-multiples---subplots)
	- [Graphiques en 3D](#graphiques-en-3d)
	- [Slide bar](#slide-bar)
- [Matplotlib.pyplot](#Matplotlib.pyplot)

<br/>

# Plotly

<br/>
Installation : <br/>
<br/>


```py
pip install plotly
```
<br/>

Documentation [Plotly](https://plotly.com/python/) .
<br/>

## Importations

<br/>

```py
from plotly.offline import plot  # pour travailler en offline!
import plotly.express as px
import plotly.graph_objects as go
from plotly.subplots import make_subplots
import pandas as pd
import numpy as np
```
<br/>

## Première approche

<br/>

### Premier exemple

```py
wide_df = px.data.medals_wide()
fig = px.bar(wide_df, x="nation", y=["gold", "silver", "bronze"],
             title="Wide-Form Input, relabelled", # le titre
             labels={"value": "count", "variable": "medal"}, # le nom des axes
             color_discrete_map={"gold": "gold", "silver": "silver", "bronze": "#c96"}, # la couleur par classe
             template="simple_white") # couleur du fond
fig.update_layout(font_family="Rockwell", # police du texte
                  showlegend=False)
fig.add_annotation(text="over target!", x="South Korea", # ajouter un texte avec une flèche
                   y=49, arrowhead=1, showarrow=True)
fig.add_shape(type="line", line_color="salmon", line_width=3, opacity=1, line_dash="dot", #najouter une ligne horizontale
              x0=0, x1=1, xref="paper", y0=40, y1=40, yref="y")
plot(fig)
```

<br/>
<p align="center">
<img width="1131" alt="Capture d’écran 2020-11-23 à 20 50 08" src="https://user-images.githubusercontent.com/63207451/100008283-83571500-2dcd-11eb-9011-a36d86335e10.png">
<p/>

### Deuxième exemple

```py
fig = go.Figure(go.Pie(
    name = "",
    title = "languages populaire",
    values = [2, 5, 3, 2.5],
    labels = ["R", "Python", "Java Script", "Matlab"],
    text = ["textA", "TextB", "TextC", "TextD"],
    hovertemplate = "%{label}: <br>Popularity: %{percent} </br> %{text}"  # ce qu'on voit en passant la souris dessus
))
plot(fig)
```
<br/>
<p align="center">
<img width="901" alt="Capture d’écran 2020-11-23 à 20 52 48" src="https://user-images.githubusercontent.com/63207451/100008564-e5177f00-2dcd-11eb-8a5a-740cc6177d08.png">
<p/>

<br/>

## Fonctions principales plotly.express

<br/>

### Scatter plot

```py
df = px.data.iris() # pandas dataframe
fig = px.scatter(df, x="sepal_width", y="sepal_length", color="species",title='Scatter')
plot(fig)
```
<br/>
<p align="center">
<img width="1184" alt="Capture d’écran 2020-11-23 à 21 41 58" src="https://user-images.githubusercontent.com/63207451/100013856-cddc8f80-2dd5-11eb-8dac-85110bdda97e.png">	
<p/>
<br/>

### Courbe de tendance et densité

```py
df = px.data.iris()
fig = px.scatter(df, x="sepal_width", y="sepal_length", color="species",marginal_y="violin",
                 marginal_x="box", trendline="ols", template="simple_white")
# trendline = ols pour lineaire et lowess pour non linéaire
plot(fig)
```
<br/>
<p align="center">
<img width="1184" alt="Capture d’écran 2020-11-23 à 21 42 12" src="https://user-images.githubusercontent.com/63207451/100014025-1300c180-2dd6-11eb-9a02-214a1174b9c8.png">
<p/>
<br/>

### Error bars

```py
df = px.data.iris()
df["e"] = df["sepal_width"]/100
fig = px.scatter(df, x="sepal_width", y="sepal_length", color="species", error_x="e", error_y="e")
plot(fig)
```
<br/>
<p align="center">
<img width="1184" alt="Capture d’écran 2020-11-23 à 21 42 24" src="https://user-images.githubusercontent.com/63207451/100014061-23b13780-2dd6-11eb-9996-866420a6b799.png">	
<p/>
<br/>

### Bar charts

```py
df = px.data.tips()
fig = px.bar(df, x="sex", y="total_bill", color="smoker", barmode="group")
# barmode="group" pour séparer les bars par color
plot(fig)
```
<br/>
<p align="center">
<img width="1187" alt="Capture d’écran 2020-11-23 à 21 42 41" src="https://user-images.githubusercontent.com/63207451/100014104-3461ad80-2dd6-11eb-8f06-02a555611f21.png">	
<p/>
<br/>

### Graphiques de corrélations

```py
df = px.data.iris()
fig = px.scatter_matrix(df, dimensions=["sepal_width", "sepal_length", "petal_width", "petal_length"], color="species")
plot(fig)
```
<br/>
<p align="center">
<img width="1187" alt="Capture d’écran 2020-11-23 à 21 43 03" src="https://user-images.githubusercontent.com/63207451/100014133-404d6f80-2dd6-11eb-9f4e-f0bca9ee9b96.png">
<p/>
<br/>

### Scatter plot avec échelle des tailles des points

```py
df = px.data.gapminder()
fig = px.scatter(df.query("year==2007"), x="gdpPercap", y="lifeExp", size="pop", color="continent",
           hover_name="country", log_x=True, size_max=60)
plot(fig)
```
<br/>
<p align="center">
<img width="1187" alt="Capture d’écran 2020-11-23 à 21 43 15" src="https://user-images.githubusercontent.com/63207451/100014179-53f8d600-2dd6-11eb-810e-d1f9c64dad45.png">	
<p/>
<br/>

### Plot avec animation

```py
df = px.data.gapminder()
fig = px.scatter(df, x="gdpPercap", y="lifeExp", animation_frame="year", animation_group="country",
           size="pop", color="continent", hover_name="country", facet_col="continent",
           log_x=True, size_max=45, range_x=[100,100000], range_y=[25,90])
# facet_col pour couper les données en plusieurs colonnes
plot(fig)
```
<br/>
<p align="center">
<img width="1187" alt="Capture d’écran 2020-11-23 à 21 43 34" src="https://user-images.githubusercontent.com/63207451/100014215-5fe49800-2dd6-11eb-9806-cd62c521106d.png">	
<p/>
<br/>

### Line charts

```py
df = px.data.gapminder()
fig = px.line(df, x="year", y="lifeExp", color="continent", line_group="country", hover_name="country",
        line_shape="spline", render_mode="svg")
plot(fig)
```
<br/>
<p align="center">
<img width="1187" alt="Capture d’écran 2020-11-23 à 21 43 48" src="https://user-images.githubusercontent.com/63207451/100014261-6d018700-2dd6-11eb-9d87-7945753a2a19.png">	
<p/>
<br/>

### Area charts

```py
df = px.data.gapminder()
fig = px.area(df, x="year", y="pop", color="continent", line_group="country")
plot(fig)
```
<br/>
<p align="center">
<img width="1187" alt="Capture d’écran 2020-11-23 à 21 43 58" src="https://user-images.githubusercontent.com/63207451/100014395-991d0800-2dd6-11eb-933a-1390d94c4e6b.png">	
<p/>
<br/>

### Pie charts

```py
df = px.data.gapminder().query("year == 2007").query("continent == 'Europe'")
df.loc[df['pop'] < 2.e6, 'country'] = 'Other countries' # Represent only large countries
fig = px.pie(df, values='pop', names='country', title='Population of European continent')
fig.update_traces(textposition='inside', textinfo='percent+label')
plot(fig)
```
<br/>
<p align="center">
<img width="1163" alt="Capture d’écran 2020-11-23 à 21 44 17" src="https://user-images.githubusercontent.com/63207451/100014448-ab974180-2dd6-11eb-8256-220db37a275e.png">	
<p/>
<br/>

### Pie charts avec partie en dehors

```py
labels = ['Oxygen','Hydrogen','Carbon_Dioxide','Nitrogen']
values = [4500, 2500, 1053, 500]

# pull is given as a fraction of the pie radius
fig = go.Figure(data=[go.Pie(labels=labels, values=values, pull=[0, 0, 0.2, 0])])
plot(fig)
```
<br/>
<p align="center">
<img width="1163" alt="Capture d’écran 2020-11-23 à 21 44 27" src="https://user-images.githubusercontent.com/63207451/100014497-ba7df400-2dd6-11eb-8931-121589445a3f.png">	
<p/>
<br/>

### Donut charts

```py
labels = ['Oxygen','Hydrogen','Carbon_Dioxide','Nitrogen']
values = [4500, 2500, 1053, 500]
# Use `hole` to create a donut-like pie chart
fig = go.Figure(data=[go.Pie(labels=labels, values=values, hole=.3)])
plot(fig)
```
<br/>
<p align="center">
<img width="1163" alt="Capture d’écran 2020-11-23 à 21 44 36" src="https://user-images.githubusercontent.com/63207451/100014528-c5d11f80-2dd6-11eb-9467-2a775d101bd8.png">	
<p/>
<br/>

### Sunburst charts

```py
df = px.data.gapminder().query("year == 2007")
fig = px.sunburst(df, path=['continent', 'country'], values='pop',
                  color='lifeExp', hover_data=['iso_alpha'])
plot(fig)
```
<br/>
<p align="center">
<img width="1163" alt="Capture d’écran 2020-11-23 à 21 44 47" src="https://user-images.githubusercontent.com/63207451/100014559-d2557800-2dd6-11eb-928f-2f080b549af9.png">	
<p/>
<br/>

### Treemaps

```py
df = px.data.gapminder().query("year == 2007")
fig = px.treemap(df, path=[px.Constant('world'), 'continent', 'country'], values='pop',
                  color='lifeExp', hover_data=['iso_alpha'])
plot(fig)
```
<br/>
<p align="center">
<img width="1163" alt="Capture d’écran 2020-11-23 à 21 44 58" src="https://user-images.githubusercontent.com/63207451/100014601-e26d5780-2dd6-11eb-92bf-97314f41bb47.png">	
<p/>
<br/>

### Histograms

```py
df = px.data.tips()
fig = px.histogram(df, x="total_bill", y="tip", color="sex", hover_data=df.columns)
plot(fig)
```
<br/>
<p align="center">
<img width="1163" alt="Capture d’écran 2020-11-23 à 21 45 11" src="https://user-images.githubusercontent.com/63207451/100014649-f5802780-2dd6-11eb-80b4-3af4f9555091.png">	
<p/>
<br/>

### Boxplots

```py
df = px.data.tips()
fig = px.box(df, x="day", y="total_bill", color="smoker", notched=True)
plot(fig)
```
<br/>
<p align="center">
<img width="1163" alt="Capture d’écran 2020-11-23 à 21 45 20" src="https://user-images.githubusercontent.com/63207451/100014681-0335ad00-2dd7-11eb-9830-34997f3030ff.png">	
<p/>
<br/>

### Violon plots

```py
df = px.data.tips()
fig = px.violin(df, y="tip", x="smoker", color="sex", box=True, points="all", hover_data=df.columns)
plot(fig)
```
<br/>
<p align="center">
<img width="1163" alt="Capture d’écran 2020-11-23 à 21 45 28" src="https://user-images.githubusercontent.com/63207451/100014702-0d57ab80-2dd7-11eb-8173-80050ccde0a5.png">	
<p/>
<br/>

### Density contours

```py
df = px.data.iris()
fig = px.density_contour(df, x="sepal_width", y="sepal_length")
plot(fig)
```
<br/>
<p align="center">
<img width="1166" alt="Capture d’écran 2020-11-23 à 21 45 43" src="https://user-images.githubusercontent.com/63207451/100014731-1a749a80-2dd7-11eb-82df-de6468a28d7d.png">	
<p/>
<br/>

### Heatmap

```py
df = px.data.iris()
fig = px.density_heatmap(df, x="sepal_width", y="sepal_length", marginal_y="histogram")
plot(fig)

fig = px.imshow([[1, 20, 30],
                 [20, 1, 60],
                 [30, 60, 1]])
plot(fig)
```
<br/>
<p align="center">
<img width="1166" alt="Capture d’écran 2020-11-23 à 21 45 59" src="https://user-images.githubusercontent.com/63207451/100014759-252f2f80-2dd7-11eb-9d56-630b029358a2.png">	
<p/>
<br/>

### Point sur une carte

```py
df = px.data.carshare()
fig = px.scatter_mapbox(df, lat="centroid_lat", lon="centroid_lon", color="peak_hour", size="car_hours",
                  color_continuous_scale=px.colors.cyclical.IceFire, size_max=15, zoom=10,
                  mapbox_style="carto-positron")
plot(fig)
```
<br/>
<p align="center">
<img width="1166" alt="Capture d’écran 2020-11-23 à 21 46 10" src="https://user-images.githubusercontent.com/63207451/100014788-311af180-2dd7-11eb-951b-a803e3e458ed.png">	
<p/>
<br/>

### Surface sur une carte

```py
df = px.data.election()
geojson = px.data.election_geojson()

fig = px.choropleth_mapbox(df, geojson=geojson, color="Bergeron",
                           locations="district", featureidkey="properties.district",
                           center={"lat": 45.5517, "lon": -73.7073},
                           mapbox_style="carto-positron", zoom=9)
plot(fig)
```
<br/>
<p align="center">
<img width="1166" alt="Capture d’écran 2020-11-23 à 21 46 25" src="https://user-images.githubusercontent.com/63207451/100014823-43952b00-2dd7-11eb-9696-d81e18e1667a.png">	
<p/>
<br/>

### Polar plots

```py
df = px.data.wind()
fig = px.scatter_polar(df, r="frequency", theta="direction", color="strength", symbol="strength",
            color_discrete_sequence=px.colors.sequential.Plasma_r)
plot(fig)
```
<br/>
<p align="center">
<img width="1166" alt="Capture d’écran 2020-11-23 à 21 46 40" src="https://user-images.githubusercontent.com/63207451/100014889-59a2eb80-2dd7-11eb-8e5f-ce79cc9a9100.png">	
<p/>
<br/>

### Polar bar charts

```py
df = px.data.wind()
fig = px.bar_polar(df, r="frequency", theta="direction", color="strength", template="plotly_dark",
            color_discrete_sequence= px.colors.sequential.Plasma_r)
plot(fig)
```
<br/>
<p align="center">
<img width="1166" alt="Capture d’écran 2020-11-23 à 21 46 55" src="https://user-images.githubusercontent.com/63207451/100014925-6aebf800-2dd7-11eb-9316-e808a0563909.png">	
<p/>
<br/>

### Radar charts

```py
df = px.data.wind()
fig = px.line_polar(df, r="frequency", theta="direction", color="strength", line_close=True,
            color_discrete_sequence=px.colors.sequential.Plasma_r)
plot(fig)
```
<br/>
<p align="center">
<img width="1166" alt="Capture d’écran 2020-11-23 à 21 47 08" src="https://user-images.githubusercontent.com/63207451/100014956-763f2380-2dd7-11eb-93fa-c342ade13527.png">	
<p/>
<br/>

### Coordonnées en 3D

```py
df = px.data.election()
fig = px.scatter_3d(df, x="Joly", y="Coderre", z="Bergeron", color="winner", size="total", hover_name="district",
                  symbol="result", color_discrete_map = {"Joly": "blue", "Bergeron": "green", "Coderre":"red"})
plot(fig)
```
<br/>
<p align="center">
<img width="1166" alt="Capture d’écran 2020-11-23 à 21 47 35" src="https://user-images.githubusercontent.com/63207451/100014978-835c1280-2dd7-11eb-8bcf-f0f2893fe247.png">	
<p/>
<br/>

### Ternary charts

```py
df = px.data.election()
fig = px.scatter_ternary(df, a="Joly", b="Coderre", c="Bergeron", color="winner", size="total", hover_name="district",
                   size_max=15, color_discrete_map = {"Joly": "blue", "Bergeron": "green", "Coderre":"red"} )
plot(fig)
```
<br/>
<p align="center">
<img width="1166" alt="Capture d’écran 2020-11-23 à 21 47 50" src="https://user-images.githubusercontent.com/63207451/100015002-8d7e1100-2dd7-11eb-8f25-14d3424f0daa.png">	
<p/>
<br/>
<p align="center">
<a href="#introduction"> retour au sommaire </a>
<p/>

<br/>
## Graphiques multiples - Subplots














# Matplotlib.pyplot
<br/>
Installation :<br/>
<br/>

```py
pip install matplotlib
```

Documentation [Matplotlib.pyplot](https://matplotlib.org/3.3.1/api/_as_gen/matplotlib.pyplot.html) .
<br/>






<p align="center">
<a href="#plotly-and-matplotlibpyplot-tutorial"> haut de la page </a>
<p/>
<p align="center">
  <a href="https://github.com/antonin-lfv" class="fancybox" ><img src="https://user-images.githubusercontent.com/63207451/97302854-e484da80-1859-11eb-9374-5b319ca51197.png" title="GitHub" width="40" height="40"></a>
  <a href="https://www.linkedin.com/in/antonin-lefevre-565b8b141" class="fancybox" ><img src="https://user-images.githubusercontent.com/63207451/97303444-b2c04380-185a-11eb-8cfc-864c33a64e4b.png" title="LinkedIn" width="40" height="40"></a>
  <a href="mailto:antoninlefevre45@icloud.com" class="fancybox" ><img src="https://user-images.githubusercontent.com/63207451/97303543-cec3e500-185a-11eb-8adc-c1364e2054a9.png" title="Mail" width="40" height="40"></a>
</p>
