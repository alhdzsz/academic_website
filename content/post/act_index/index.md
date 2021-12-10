---
title: Índice de Transparencia en Residencias
subtitle: Este apéndice en línea contiene los calculos y códigos para el índice de transparencia en residencias en España. 

# Summary for listings and search engines
summary: Este apéndice en línea contiene los calculos y códigos para el índice de transparencia en residencias en España. Los datos fueron tomados de *Transparency in nursing home services, a legal requirement and an issue of concern before and during COVID-19 in Spain?* Pérez-durán y Hernández-Sánchez (2021).

# Image
image:
  caption: 'Image credit: [**Unsplash/Wilhelm Gunkel**](https://unsplash.com/photos/3VQ4AfOKCVc)'
  focal_point: ""
  preview_only: false
  
# Link this post with a project
projects: []

# Date published
date: "2021-10-12T00:00:00Z"

# Date updated
lastmod: "2021-10-12T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

authors:
- admin
- Ixchel Pérez Dúran
- Julia García Puig

tags:
- R
- Quantitative Text Analysis
- Transparency

categories:
- Maps
- Policy Papers
- Data Visualization
---

</head>

<body>


<div class="container-fluid main-container">




<div id="header">



<h1 class="title toc-ignore">Indice de Transparencia ACT-España</h1>
<h4 class="author">Alfredo Hernandez Sanchez, Ixchel Perez Duran, Julia Garcia Puig</h4>
<h4 class="date">12/8/2021</h4>

</div>


<div id="cálculos-del-índice" class="section level2">
<h2>Cálculos del Índice</h2>
<pre class="r"><code># Raw Counts (estructuras, procesos, resultados)
weights1 = c(7/26, 13/26, 6/26)

df = df %&gt;% 
  mutate(
    # Raw Percentage
    est_perc1 = est_count / 7,
    pro_perc1 = pro_count / 13,
    res_perc1 = res_count / 6,
    # Adjusted Percentage
    est_perc2 = est_count / 3,
    pro_perc2 = pro_count / 11,
    res_perc2 = res_count / 4,
  ) %&gt;% 
  rowwise() %&gt;% 
  mutate(
    # Raw Index
    index_act = mean(c(est_perc1, pro_perc1, res_perc1)),
    # Weighted Index
    index_act_w = weighted.mean(c(est_perc1, pro_perc1, res_perc1), w = weights1)
  ) %&gt;% 
  ungroup() %&gt;% 
  mutate(
    # W Adjusted Index
    index_act_adj = (index_act_w - min(index_act_w)) / (max(index_act_w) - min(index_act_w))
  )</code></pre>
<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:300px; overflow-x: scroll; width:100%; ">
<table class="table" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">
Comunidad
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
est_count
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
pro_count
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
res_count
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
est_perc1
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
pro_perc1
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
res_perc1
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
est_perc2
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
pro_perc2
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
res_perc2
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
index_act
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
index_act_w
</th>
<th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;">
index_act_adj
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Andalucía
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.29
</td>
<td style="text-align:right;">
0.38
</td>
<td style="text-align:right;">
0.17
</td>
<td style="text-align:right;">
0.67
</td>
<td style="text-align:right;">
0.45
</td>
<td style="text-align:right;">
0.25
</td>
<td style="text-align:right;">
0.28
</td>
<td style="text-align:right;">
0.31
</td>
<td style="text-align:right;">
0.57
</td>
</tr>
<tr>
<td style="text-align:left;">
Aragón
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.14
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.17
</td>
<td style="text-align:right;">
0.33
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.25
</td>
<td style="text-align:right;">
0.10
</td>
<td style="text-align:right;">
0.08
</td>
<td style="text-align:right;">
0.14
</td>
</tr>
<tr>
<td style="text-align:left;">
Principado de Asturias
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.29
</td>
<td style="text-align:right;">
0.54
</td>
<td style="text-align:right;">
0.17
</td>
<td style="text-align:right;">
0.67
</td>
<td style="text-align:right;">
0.64
</td>
<td style="text-align:right;">
0.25
</td>
<td style="text-align:right;">
0.33
</td>
<td style="text-align:right;">
0.38
</td>
<td style="text-align:right;">
0.71
</td>
</tr>
<tr>
<td style="text-align:left;">
Islas Baleares
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
0.29
</td>
<td style="text-align:right;">
0.62
</td>
<td style="text-align:right;">
0.33
</td>
<td style="text-align:right;">
0.67
</td>
<td style="text-align:right;">
0.73
</td>
<td style="text-align:right;">
0.50
</td>
<td style="text-align:right;">
0.41
</td>
<td style="text-align:right;">
0.46
</td>
<td style="text-align:right;">
0.86
</td>
</tr>
<tr>
<td style="text-align:left;">
Canarias
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
9
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0.29
</td>
<td style="text-align:right;">
0.69
</td>
<td style="text-align:right;">
0.50
</td>
<td style="text-align:right;">
0.67
</td>
<td style="text-align:right;">
0.82
</td>
<td style="text-align:right;">
0.75
</td>
<td style="text-align:right;">
0.49
</td>
<td style="text-align:right;">
0.54
</td>
<td style="text-align:right;">
1.00
</td>
</tr>
<tr>
<td style="text-align:left;">
Cantabria
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
0.14
</td>
<td style="text-align:right;">
0.15
</td>
<td style="text-align:right;">
0.33
</td>
<td style="text-align:right;">
0.33
</td>
<td style="text-align:right;">
0.18
</td>
<td style="text-align:right;">
0.50
</td>
<td style="text-align:right;">
0.21
</td>
<td style="text-align:right;">
0.19
</td>
<td style="text-align:right;">
0.36
</td>
</tr>
<tr>
<td style="text-align:left;">
Castilla y León
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.14
</td>
<td style="text-align:right;">
0.54
</td>
<td style="text-align:right;">
0.17
</td>
<td style="text-align:right;">
0.33
</td>
<td style="text-align:right;">
0.64
</td>
<td style="text-align:right;">
0.25
</td>
<td style="text-align:right;">
0.28
</td>
<td style="text-align:right;">
0.35
</td>
<td style="text-align:right;">
0.64
</td>
</tr>
<tr>
<td style="text-align:left;">
Castilla-La Mancha
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.38
</td>
<td style="text-align:right;">
0.17
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.45
</td>
<td style="text-align:right;">
0.25
</td>
<td style="text-align:right;">
0.18
</td>
<td style="text-align:right;">
0.23
</td>
<td style="text-align:right;">
0.43
</td>
</tr>
<tr>
<td style="text-align:left;">
Cataluña
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.23
</td>
<td style="text-align:right;">
0.17
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.27
</td>
<td style="text-align:right;">
0.25
</td>
<td style="text-align:right;">
0.13
</td>
<td style="text-align:right;">
0.15
</td>
<td style="text-align:right;">
0.29
</td>
</tr>
<tr>
<td style="text-align:left;">
Comunidad Valenciana
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0.29
</td>
<td style="text-align:right;">
0.46
</td>
<td style="text-align:right;">
0.50
</td>
<td style="text-align:right;">
0.67
</td>
<td style="text-align:right;">
0.55
</td>
<td style="text-align:right;">
0.75
</td>
<td style="text-align:right;">
0.42
</td>
<td style="text-align:right;">
0.42
</td>
<td style="text-align:right;">
0.79
</td>
</tr>
<tr>
<td style="text-align:left;">
Extremadura
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0.14
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.33
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.05
</td>
<td style="text-align:right;">
0.04
</td>
<td style="text-align:right;">
0.07
</td>
</tr>
<tr>
<td style="text-align:left;">
Galicia
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.00
</td>
</tr>
<tr>
<td style="text-align:left;">
Comunidad de Madrid
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0.14
</td>
<td style="text-align:right;">
0.08
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.33
</td>
<td style="text-align:right;">
0.09
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.07
</td>
<td style="text-align:right;">
0.08
</td>
<td style="text-align:right;">
0.14
</td>
</tr>
<tr>
<td style="text-align:left;">
Región de Murcia
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0.29
</td>
<td style="text-align:right;">
0.54
</td>
<td style="text-align:right;">
0.50
</td>
<td style="text-align:right;">
0.67
</td>
<td style="text-align:right;">
0.64
</td>
<td style="text-align:right;">
0.75
</td>
<td style="text-align:right;">
0.44
</td>
<td style="text-align:right;">
0.46
</td>
<td style="text-align:right;">
0.86
</td>
</tr>
<tr>
<td style="text-align:left;">
Comunidad Foral de Navarra
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.46
</td>
<td style="text-align:right;">
0.17
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.55
</td>
<td style="text-align:right;">
0.25
</td>
<td style="text-align:right;">
0.21
</td>
<td style="text-align:right;">
0.27
</td>
<td style="text-align:right;">
0.50
</td>
</tr>
<tr>
<td style="text-align:left;">
País Vasco
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
0.29
</td>
<td style="text-align:right;">
0.54
</td>
<td style="text-align:right;">
0.33
</td>
<td style="text-align:right;">
0.67
</td>
<td style="text-align:right;">
0.64
</td>
<td style="text-align:right;">
0.50
</td>
<td style="text-align:right;">
0.39
</td>
<td style="text-align:right;">
0.42
</td>
<td style="text-align:right;">
0.79
</td>
</tr>
<tr>
<td style="text-align:left;">
La Rioja
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.29
</td>
<td style="text-align:right;">
0.46
</td>
<td style="text-align:right;">
0.17
</td>
<td style="text-align:right;">
0.67
</td>
<td style="text-align:right;">
0.55
</td>
<td style="text-align:right;">
0.25
</td>
<td style="text-align:right;">
0.30
</td>
<td style="text-align:right;">
0.35
</td>
<td style="text-align:right;">
0.64
</td>
</tr>
</tbody>
</table>
</div>
</div>
<div id="resultados" class="section level2">
<h2>Resultados</h2>
<p>La tabla y el mapa muestran los resultados del Índice de Transparencia en Residencias de Mayores (TRM) al nivel de Comunidad Autónoma. El índice esta compuesto por tres pilares: Estructuras, Procesos y Resultados. Estos pilares reflejan la cantidad de requisitos legales de transparencia que se cumplen en cada Comunidad Autónoma. Estos pilares de transparencia y sus indicadores están explicados a mayor detalle en Pérez-Durán y Hernández-Sánchez (2021). El promedio de los pilares son 0.18 en Estructuras (de 7 indicadores), 0.36 en Procesos (de 14 indicadores) y 0.23 en Resultados (de 6 indicadores). Finalmente, el promedio del Índice TRM es de tan solo 0.25. El caso de Galicia es especialmente preocupante ya que aún no se cumplen con ninguno de los 27 indicadores de transparencia.</p>
<table class="huxtable" style="border-collapse: collapse; border: 0px; margin-bottom: 2em; margin-top: 2em; ; margin-left: auto; margin-right: auto;  " id="tab:unnamed-chunk-2">
<caption style="caption-side: top; text-align: center;">Indice de Transparencia en Residencias de Mayores</caption><col><col><col><col><col><tr>
<th style="vertical-align: top; text-align: left; white-space: normal; border-style: solid solid solid solid; border-width: 0pt 0pt 0.4pt 0pt;    padding: 3pt 3pt 3pt 3pt; font-weight: bold;">Comunidad</th><th style="vertical-align: top; text-align: right; white-space: normal; border-style: solid solid solid solid; border-width: 0pt 0pt 0.4pt 0pt;    padding: 3pt 3pt 3pt 3pt; font-weight: bold;">Estructuras</th><th style="vertical-align: top; text-align: right; white-space: normal; border-style: solid solid solid solid; border-width: 0pt 0pt 0.4pt 0pt;    padding: 3pt 3pt 3pt 3pt; font-weight: bold;">Procesos</th><th style="vertical-align: top; text-align: right; white-space: normal; border-style: solid solid solid solid; border-width: 0pt 0pt 0.4pt 0pt;    padding: 3pt 3pt 3pt 3pt; font-weight: bold;">Resultados</th><th style="vertical-align: top; text-align: right; white-space: normal; border-style: solid solid solid solid; border-width: 0pt 0pt 0.4pt 0pt;    padding: 3pt 3pt 3pt 3pt; font-weight: bold;">Indice</th></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; border-style: solid solid solid solid; border-width: 0.4pt 0pt 0pt 0pt;    padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">Andalucía</td><td style="vertical-align: top; text-align: right; white-space: normal; border-style: solid solid solid solid; border-width: 0.4pt 0pt 0pt 0pt;    padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.29</td><td style="vertical-align: top; text-align: right; white-space: normal; border-style: solid solid solid solid; border-width: 0.4pt 0pt 0pt 0pt;    padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.38</td><td style="vertical-align: top; text-align: right; white-space: normal; border-style: solid solid solid solid; border-width: 0.4pt 0pt 0pt 0pt;    padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.17</td><td style="vertical-align: top; text-align: right; white-space: normal; border-style: solid solid solid solid; border-width: 0.4pt 0pt 0pt 0pt;    padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.28</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">Aragón</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.14</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.17</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.10</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">Principado de Asturias</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.29</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.54</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.17</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.33</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">Islas Baleares</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.29</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.62</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.33</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.41</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">Canarias</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.29</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.69</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.50</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.49</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">Cantabria</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.14</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.15</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.33</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.21</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">Castilla y León</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.14</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.54</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.17</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.28</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">Castilla-La Mancha</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.38</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.17</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.18</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">Cataluña</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.23</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.17</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.13</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">Comunidad Valenciana</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.29</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.46</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.50</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.42</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">Extremadura</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.14</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.05</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">Galicia</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.00</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">Comunidad de Madrid</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.14</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.08</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.07</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">Región de Murcia</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.29</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.54</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.50</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.44</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">Comunidad Foral de Navarra</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.46</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.17</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.21</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">País Vasco</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.29</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.54</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.33</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.39</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">La Rioja</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.29</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.46</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.17</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.30</td></tr>
</table>

<pre class="r"><code>df %&gt;%
  select(Comunidad, est_perc1, pro_perc1, res_perc1, index_act) %&gt;% 
  rename(
    Estructuras = est_perc1,
    Procesos = pro_perc1,
    Resultados = res_perc1,
    Indice = index_act
  ) %&gt;% 
  gather(Indicator, Value, Estructuras:Resultados) %&gt;% 
  ggplot(aes(x = Comunidad, y = Value)) +
  geom_col(aes(fill = Indicator), position = &quot;dodge&quot;) +
  geom_col(data = df, aes(x = Comunidad, y = index_act), color = &quot;black&quot;, fill = NA) +
  geom_label(data = df, aes(x = Comunidad, y = index_act, label = round(index_act, digits = 2)), 
             color = &quot;black&quot;,
             size = 2) +
  coord_cartesian(ylim = 0:1) +
  labs(x = NULL, y = NULL, fill = &quot;Pilar:&quot;,
       title = &quot;Índice de Transparencia en Residencias de Mayores&quot;,
       caption = &quot;Fuente: Perez-Duran &amp; Hernandez-Sanchez (2021)&quot;) +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 35, size = 6.5),
        axis.ticks.x = element_line(color = &quot;gray90&quot;),
        axis.ticks.length.x = unit(.5, &quot;cm&quot;),
        panel.grid = element_blank(),
        panel.grid.major.x = element_line(color = &quot;gray90&quot;),
        legend.position = &quot;top&quot;,
        plot.background = element_rect(fill = &quot;white&quot;, color = NA)
        )  </code></pre>
<div class="figure" style="text-align: center">
<img src="data:image/png;base64,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" alt="Pilares en Comunidades Autonomas" width="100%" />
<p class="caption">
Pilares en Comunidades Autonomas
</p>
</div>
<pre class="r"><code>spain_communities %&gt;% 
  ggplot() + 
  geom_sf() + 
  geom_sf(aes(fill = index_act), show.legend = F) +   
  scale_fill_viridis_c(option = &quot;plasma&quot;,
                       breaks=c(0,.25,.50,.75,1)) +
  geom_label(aes(X, Y, label = NAME_1, color = index_act), 
             size = 3, 
             fontface = &quot;bold&quot;,
             show.legend = F) +
  scale_color_viridis_c(option = &quot;plasma&quot;) +
  coord_sf(xlim = c(-19, -13),
           ylim = c(27, 30),
           expand = FALSE) +
  theme_void() +
  theme(plot.background = element_rect(fill = &quot;aliceblue&quot;)) -&gt; sub_map1

world %&gt;% 
  ggplot() + 
  geom_sf(color = NA, fill = &quot;antiquewhite&quot;) +
  geom_sf(data = spain_communities,
          aes(fill = index_act)) +
  scale_fill_viridis_c(option = &quot;plasma&quot;,
                       breaks=c(0,.25,.50,.75,1)) +
    coord_sf(xlim = c(-10, 5),
           ylim = c(35, 45),
           expand = FALSE) +
  geom_label(data = spain_communities, 
             aes(X, Y, label = NAME_1, color = index_act), 
             size = 3, 
             fontface = &quot;bold&quot;,
             show.legend = F) +
  scale_color_viridis_c(option = &quot;plasma&quot;) +
  annotation_custom(
    grob = ggplotGrob(sub_map1),
    xmin = 0,
    xmax = 4,
    ymin = 35,
    ymax = 37) +
  theme_void() +
  labs(fill = &quot;Indice: \n&quot;,
       title = &quot;Índice de Transparencia en Residencias de Mayores&quot;,
       subtitle = sprintf(&quot;Promedio: %s, Rango: 0 - 1&quot;, round(mean(df$index_act), digits = 2)),
       caption = &quot;Fuente: Perez-Duran &amp; Hernandez-Sanchez (2021)&quot;) +
  theme(legend.position = &quot;bottom&quot;, 
        legend.key.width= unit(1, &#39;cm&#39;),
        legend.key.height = unit(.2, &#39;cm&#39;),
        legend.text = element_text(size = 7),
        panel.grid.major = element_line(color = gray(.8), linetype = &quot;dashed&quot;, size = 0.3),
        panel.background = element_rect(fill = &quot;aliceblue&quot;, color = NA),
        plot.background = element_rect(fill = &quot;white&quot;, color = NA)
        )  </code></pre>
<div class="figure" style="text-align: center">
<img src="data:image/png;base64,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" alt="Mapa de Comunidades Autonomas" width="100%" />
<p class="caption">
Mapa de Comunidades Autonomas
</p>
</div>
</div>




</div>

<script>

// add bootstrap table styles to pandoc tables
function bootstrapStylePandocTables() {
  $('tr.odd').parent('tbody').parent('table').addClass('table table-condensed');
}
$(document).ready(function () {
  bootstrapStylePandocTables();
});


</script>

<!-- tabsets -->

<script>
$(document).ready(function () {
  window.buildTabsets("TOC");
});

$(document).ready(function () {
  $('.tabset-dropdown > .nav-tabs > li').click(function () {
    $(this).parent().toggleClass('nav-tabs-open');
  });
});
</script>

<!-- code folding -->


<!-- dynamically load mathjax for compatibility with self-contained -->
<script>
  (function () {
    var script = document.createElement("script");
    script.type = "text/javascript";
    script.src  = "https://mathjax.rstudio.com/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML";
    document.getElementsByTagName("head")[0].appendChild(script);
  })();
</script>

</body>
</html>
