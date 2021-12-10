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

<div class="btn-group pull-right float-right">
<button type="button" class="btn btn-default btn-xs btn-secondary btn-sm dropdown-toggle" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false"><span>Code</span> <span class="caret"></span></button>
<ul class="dropdown-menu dropdown-menu-right" style="min-width: 50px;">
<li><a id="rmd-show-all-code" href="#">Show All Code</a></li>
<li><a id="rmd-hide-all-code" href="#">Hide All Code</a></li>
</ul>
</div>



<h1 class="title toc-ignore">Indice de Transparencia ACT-España</h1>
<h4 class="author">Alfredo Hernandez Sanchez, Ixchel Perez Duran, Julia Garcia Puig</h4>
<h4 class="date">12/8/2021</h4>

</div>


<div id="cálculos-del-índice" class="section level2">
<h2>Cálculos del Índice</h2>
<div class="sourceCode" id="cb1"><pre class="sourceCode r"><code class="sourceCode r"><span id="cb1-1"><a href="#cb1-1"></a><span class="co"># Raw Counts (estructuras, procesos, resultados)</span></span>
<span id="cb1-2"><a href="#cb1-2"></a>weights1 =<span class="st"> </span><span class="kw">c</span>(<span class="dv">7</span><span class="op">/</span><span class="dv">27</span>, <span class="dv">14</span><span class="op">/</span><span class="dv">27</span>, <span class="dv">6</span><span class="op">/</span><span class="dv">27</span>)</span>
<span id="cb1-3"><a href="#cb1-3"></a></span>
<span id="cb1-4"><a href="#cb1-4"></a>df =<span class="st"> </span>df <span class="op">%&gt;%</span><span class="st"> </span></span>
<span id="cb1-5"><a href="#cb1-5"></a><span class="st">  </span><span class="kw">mutate</span>(</span>
<span id="cb1-6"><a href="#cb1-6"></a>    <span class="co"># Raw Percentage</span></span>
<span id="cb1-7"><a href="#cb1-7"></a>    <span class="dt">est_perc1 =</span> est_count <span class="op">/</span><span class="st"> </span><span class="dv">7</span>,</span>
<span id="cb1-8"><a href="#cb1-8"></a>    <span class="dt">pro_perc1 =</span> pro_count <span class="op">/</span><span class="st"> </span><span class="dv">14</span>,</span>
<span id="cb1-9"><a href="#cb1-9"></a>    <span class="dt">res_perc1 =</span> res_count <span class="op">/</span><span class="st"> </span><span class="dv">6</span>,</span>
<span id="cb1-10"><a href="#cb1-10"></a>    <span class="co"># Adjusted Percentage</span></span>
<span id="cb1-11"><a href="#cb1-11"></a>    <span class="dt">est_perc2 =</span> est_count <span class="op">/</span><span class="st"> </span><span class="dv">3</span>,</span>
<span id="cb1-12"><a href="#cb1-12"></a>    <span class="dt">pro_perc2 =</span> pro_count <span class="op">/</span><span class="st"> </span><span class="dv">12</span>,</span>
<span id="cb1-13"><a href="#cb1-13"></a>    <span class="dt">res_perc2 =</span> res_count <span class="op">/</span><span class="st"> </span><span class="dv">4</span>,</span>
<span id="cb1-14"><a href="#cb1-14"></a>  ) <span class="op">%&gt;%</span><span class="st"> </span></span>
<span id="cb1-15"><a href="#cb1-15"></a><span class="st">  </span><span class="kw">rowwise</span>() <span class="op">%&gt;%</span><span class="st"> </span></span>
<span id="cb1-16"><a href="#cb1-16"></a><span class="st">  </span><span class="kw">mutate</span>(</span>
<span id="cb1-17"><a href="#cb1-17"></a>    <span class="co"># Raw Index</span></span>
<span id="cb1-18"><a href="#cb1-18"></a>    <span class="dt">index_act =</span> <span class="kw">mean</span>(<span class="kw">c</span>(est_perc1, pro_perc1, res_perc1)),</span>
<span id="cb1-19"><a href="#cb1-19"></a>    <span class="co"># Weighted Index</span></span>
<span id="cb1-20"><a href="#cb1-20"></a>    <span class="dt">index_act_w =</span> <span class="kw">weighted.mean</span>(<span class="kw">c</span>(est_perc1, pro_perc1, res_perc1), <span class="dt">w =</span> weights1)</span>
<span id="cb1-21"><a href="#cb1-21"></a>  ) <span class="op">%&gt;%</span><span class="st"> </span></span>
<span id="cb1-22"><a href="#cb1-22"></a><span class="st">  </span><span class="kw">ungroup</span>() <span class="op">%&gt;%</span><span class="st"> </span></span>
<span id="cb1-23"><a href="#cb1-23"></a><span class="st">  </span><span class="kw">mutate</span>(</span>
<span id="cb1-24"><a href="#cb1-24"></a>    <span class="co"># W Adjusted Index</span></span>
<span id="cb1-25"><a href="#cb1-25"></a>    <span class="dt">index_act_adj =</span> (index_act_w <span class="op">-</span><span class="st"> </span><span class="kw">min</span>(index_act_w)) <span class="op">/</span><span class="st"> </span>(<span class="kw">max</span>(index_act_w) <span class="op">-</span><span class="st"> </span><span class="kw">min</span>(index_act_w))</span>
<span id="cb1-26"><a href="#cb1-26"></a>  )</span></code></pre></div>
<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:300px; overflow-x: scroll; width:80%; ">
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
0.36
</td>
<td style="text-align:right;">
0.17
</td>
<td style="text-align:right;">
0.67
</td>
<td style="text-align:right;">
0.42
</td>
<td style="text-align:right;">
0.25
</td>
<td style="text-align:right;">
0.27
</td>
<td style="text-align:right;">
0.30
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
0.07
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
0.50
</td>
<td style="text-align:right;">
0.17
</td>
<td style="text-align:right;">
0.67
</td>
<td style="text-align:right;">
0.58
</td>
<td style="text-align:right;">
0.25
</td>
<td style="text-align:right;">
0.32
</td>
<td style="text-align:right;">
0.37
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
0.57
</td>
<td style="text-align:right;">
0.33
</td>
<td style="text-align:right;">
0.67
</td>
<td style="text-align:right;">
0.67
</td>
<td style="text-align:right;">
0.50
</td>
<td style="text-align:right;">
0.40
</td>
<td style="text-align:right;">
0.44
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
0.64
</td>
<td style="text-align:right;">
0.50
</td>
<td style="text-align:right;">
0.67
</td>
<td style="text-align:right;">
0.75
</td>
<td style="text-align:right;">
0.75
</td>
<td style="text-align:right;">
0.48
</td>
<td style="text-align:right;">
0.52
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
0.14
</td>
<td style="text-align:right;">
0.33
</td>
<td style="text-align:right;">
0.33
</td>
<td style="text-align:right;">
0.17
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
0.50
</td>
<td style="text-align:right;">
0.17
</td>
<td style="text-align:right;">
0.33
</td>
<td style="text-align:right;">
0.58
</td>
<td style="text-align:right;">
0.25
</td>
<td style="text-align:right;">
0.27
</td>
<td style="text-align:right;">
0.33
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
0.36
</td>
<td style="text-align:right;">
0.17
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.42
</td>
<td style="text-align:right;">
0.25
</td>
<td style="text-align:right;">
0.17
</td>
<td style="text-align:right;">
0.22
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
0.21
</td>
<td style="text-align:right;">
0.17
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.25
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
0.43
</td>
<td style="text-align:right;">
0.50
</td>
<td style="text-align:right;">
0.67
</td>
<td style="text-align:right;">
0.50
</td>
<td style="text-align:right;">
0.75
</td>
<td style="text-align:right;">
0.40
</td>
<td style="text-align:right;">
0.41
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
0.07
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.33
</td>
<td style="text-align:right;">
0.08
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.07
</td>
<td style="text-align:right;">
0.07
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
0.50
</td>
<td style="text-align:right;">
0.50
</td>
<td style="text-align:right;">
0.67
</td>
<td style="text-align:right;">
0.58
</td>
<td style="text-align:right;">
0.75
</td>
<td style="text-align:right;">
0.43
</td>
<td style="text-align:right;">
0.44
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
0.43
</td>
<td style="text-align:right;">
0.17
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.50
</td>
<td style="text-align:right;">
0.25
</td>
<td style="text-align:right;">
0.20
</td>
<td style="text-align:right;">
0.26
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
0.50
</td>
<td style="text-align:right;">
0.33
</td>
<td style="text-align:right;">
0.67
</td>
<td style="text-align:right;">
0.58
</td>
<td style="text-align:right;">
0.50
</td>
<td style="text-align:right;">
0.37
</td>
<td style="text-align:right;">
0.41
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
0.43
</td>
<td style="text-align:right;">
0.17
</td>
<td style="text-align:right;">
0.67
</td>
<td style="text-align:right;">
0.50
</td>
<td style="text-align:right;">
0.25
</td>
<td style="text-align:right;">
0.29
</td>
<td style="text-align:right;">
0.33
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
<p>La tabla y el mapa muestran los resultados del Índice de Transparencia en Residencias de Mayores (TRM) al nivel de Comunidad Autónoma. El índice esta compuesto por tres pilares: Estructuras, Procesos y Resultados. Estos pilares reflejan la cantidad de requisitos legales de transparencia que se cumplen en cada Comunidad Autónoma. Estos pilares de transparencia y sus indicadores están explicados a mayor detalle en Pérez-Durán y Hernández-Sánchez (2021). El promedio de los pilares son 0.18 en Estructuras (de 7 indicadores), 0.33 en Procesos (de 14 indicadores) y 0.23 en Resultados (de 6 indicadores). Finalmente, el promedio del Índice TRM es de tan solo 0.24. El caso de Galicia es especialmente preocupante ya que aún no se cumplen con ninguno de los 27 indicadores de transparencia.</p>
<table class="huxtable" style="border-collapse: collapse; border: 0px; margin-bottom: 2em; margin-top: 2em; ; margin-left: auto; margin-right: auto;  " id="tab:unnamed-chunk-2">
<caption style="caption-side: top; text-align: center;">Indice de Transparencia en Residencias de Mayores</caption><col><col><col><col><col><tr>
<th style="vertical-align: top; text-align: left; white-space: normal; border-style: solid solid solid solid; border-width: 0pt 0pt 0.4pt 0pt;    padding: 3pt 3pt 3pt 3pt; font-weight: bold;">Comunidad</th><th style="vertical-align: top; text-align: right; white-space: normal; border-style: solid solid solid solid; border-width: 0pt 0pt 0.4pt 0pt;    padding: 3pt 3pt 3pt 3pt; font-weight: bold;">Estructuras</th><th style="vertical-align: top; text-align: right; white-space: normal; border-style: solid solid solid solid; border-width: 0pt 0pt 0.4pt 0pt;    padding: 3pt 3pt 3pt 3pt; font-weight: bold;">Procesos</th><th style="vertical-align: top; text-align: right; white-space: normal; border-style: solid solid solid solid; border-width: 0pt 0pt 0.4pt 0pt;    padding: 3pt 3pt 3pt 3pt; font-weight: bold;">Resultados</th><th style="vertical-align: top; text-align: right; white-space: normal; border-style: solid solid solid solid; border-width: 0pt 0pt 0.4pt 0pt;    padding: 3pt 3pt 3pt 3pt; font-weight: bold;">Indice</th></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; border-style: solid solid solid solid; border-width: 0.4pt 0pt 0pt 0pt;    padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">Andalucía</td><td style="vertical-align: top; text-align: right; white-space: normal; border-style: solid solid solid solid; border-width: 0.4pt 0pt 0pt 0pt;    padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.29</td><td style="vertical-align: top; text-align: right; white-space: normal; border-style: solid solid solid solid; border-width: 0.4pt 0pt 0pt 0pt;    padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.36</td><td style="vertical-align: top; text-align: right; white-space: normal; border-style: solid solid solid solid; border-width: 0.4pt 0pt 0pt 0pt;    padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.17</td><td style="vertical-align: top; text-align: right; white-space: normal; border-style: solid solid solid solid; border-width: 0.4pt 0pt 0pt 0pt;    padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.27</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">Aragón</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.14</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.17</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.10</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">Principado de Asturias</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.29</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.50</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.17</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.32</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">Islas Baleares</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.29</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.57</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.33</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.40</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">Canarias</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.29</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.64</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.50</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.48</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">Cantabria</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.14</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.14</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.33</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.21</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">Castilla y León</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.14</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.50</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.17</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.27</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">Castilla-La Mancha</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.36</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.17</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.17</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">Cataluña</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.21</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.17</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.13</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">Comunidad Valenciana</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.29</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.43</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.50</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.40</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">Extremadura</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.14</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.05</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">Galicia</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.00</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">Comunidad de Madrid</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.14</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.07</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.07</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">Región de Murcia</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.29</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.50</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.50</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.43</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">Comunidad Foral de Navarra</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.00</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.43</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.17</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.20</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">País Vasco</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.29</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.50</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.33</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; font-weight: normal;">0.37</td></tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">La Rioja</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.29</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.43</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.17</td><td style="vertical-align: top; text-align: right; white-space: normal; padding: 3pt 3pt 3pt 3pt; background-color: rgb(242, 242, 242); font-weight: normal;">0.29</td></tr>
</table>

<div class="sourceCode" id="cb2"><pre class="sourceCode r"><code class="sourceCode r"><span id="cb2-1"><a href="#cb2-1"></a>df <span class="op">%&gt;%</span></span>
<span id="cb2-2"><a href="#cb2-2"></a><span class="st">  </span><span class="kw">select</span>(Comunidad, est_perc1, pro_perc1, res_perc1, index_act) <span class="op">%&gt;%</span><span class="st"> </span></span>
<span id="cb2-3"><a href="#cb2-3"></a><span class="st">  </span><span class="kw">rename</span>(</span>
<span id="cb2-4"><a href="#cb2-4"></a>    <span class="dt">Estructuras =</span> est_perc1,</span>
<span id="cb2-5"><a href="#cb2-5"></a>    <span class="dt">Procesos =</span> pro_perc1,</span>
<span id="cb2-6"><a href="#cb2-6"></a>    <span class="dt">Resultados =</span> res_perc1,</span>
<span id="cb2-7"><a href="#cb2-7"></a>    <span class="dt">Indice =</span> index_act</span>
<span id="cb2-8"><a href="#cb2-8"></a>  ) <span class="op">%&gt;%</span><span class="st"> </span></span>
<span id="cb2-9"><a href="#cb2-9"></a><span class="st">  </span><span class="kw">gather</span>(Indicator, Value, Estructuras<span class="op">:</span>Resultados) <span class="op">%&gt;%</span><span class="st"> </span></span>
<span id="cb2-10"><a href="#cb2-10"></a><span class="st">  </span><span class="kw">ggplot</span>(<span class="kw">aes</span>(<span class="dt">x =</span> Comunidad, <span class="dt">y =</span> Value)) <span class="op">+</span></span>
<span id="cb2-11"><a href="#cb2-11"></a><span class="st">  </span><span class="kw">geom_col</span>(<span class="kw">aes</span>(<span class="dt">fill =</span> Indicator), <span class="dt">position =</span> <span class="st">&quot;dodge&quot;</span>) <span class="op">+</span></span>
<span id="cb2-12"><a href="#cb2-12"></a><span class="st">  </span><span class="kw">geom_col</span>(<span class="dt">data =</span> df, <span class="kw">aes</span>(<span class="dt">x =</span> Comunidad, <span class="dt">y =</span> index_act), <span class="dt">color =</span> <span class="st">&quot;black&quot;</span>, <span class="dt">fill =</span> <span class="ot">NA</span>) <span class="op">+</span></span>
<span id="cb2-13"><a href="#cb2-13"></a><span class="st">  </span><span class="kw">geom_label</span>(<span class="dt">data =</span> df, <span class="kw">aes</span>(<span class="dt">x =</span> Comunidad, <span class="dt">y =</span> index_act, <span class="dt">label =</span> <span class="kw">round</span>(index_act, <span class="dt">digits =</span> <span class="dv">2</span>)), </span>
<span id="cb2-14"><a href="#cb2-14"></a>             <span class="dt">color =</span> <span class="st">&quot;black&quot;</span>,</span>
<span id="cb2-15"><a href="#cb2-15"></a>             <span class="dt">size =</span> <span class="dv">2</span>) <span class="op">+</span></span>
<span id="cb2-16"><a href="#cb2-16"></a><span class="st">  </span><span class="kw">coord_cartesian</span>(<span class="dt">ylim =</span> <span class="dv">0</span><span class="op">:</span><span class="dv">1</span>) <span class="op">+</span></span>
<span id="cb2-17"><a href="#cb2-17"></a><span class="st">  </span><span class="kw">labs</span>(<span class="dt">x =</span> <span class="ot">NULL</span>, <span class="dt">y =</span> <span class="ot">NULL</span>, <span class="dt">fill =</span> <span class="st">&quot;Pilar:&quot;</span>,</span>
<span id="cb2-18"><a href="#cb2-18"></a>       <span class="dt">title =</span> <span class="st">&quot;Índice de Transparencia en Residencias de Mayores&quot;</span>,</span>
<span id="cb2-19"><a href="#cb2-19"></a>       <span class="dt">caption =</span> <span class="st">&quot;Fuente: Perez-Duran &amp; Hernandez-Sanchez (2021)&quot;</span>) <span class="op">+</span></span>
<span id="cb2-20"><a href="#cb2-20"></a><span class="st">  </span><span class="kw">theme_minimal</span>() <span class="op">+</span></span>
<span id="cb2-21"><a href="#cb2-21"></a><span class="st">  </span><span class="kw">theme</span>(<span class="dt">axis.text.x =</span> <span class="kw">element_text</span>(<span class="dt">angle =</span> <span class="dv">35</span>, <span class="dt">size =</span> <span class="fl">6.5</span>),</span>
<span id="cb2-22"><a href="#cb2-22"></a>        <span class="dt">axis.ticks.x =</span> <span class="kw">element_line</span>(<span class="dt">color =</span> <span class="st">&quot;gray90&quot;</span>),</span>
<span id="cb2-23"><a href="#cb2-23"></a>        <span class="dt">axis.ticks.length.x =</span> <span class="kw">unit</span>(.<span class="dv">5</span>, <span class="st">&quot;cm&quot;</span>),</span>
<span id="cb2-24"><a href="#cb2-24"></a>        <span class="dt">panel.grid =</span> <span class="kw">element_blank</span>(),</span>
<span id="cb2-25"><a href="#cb2-25"></a>        <span class="dt">panel.grid.major.x =</span> <span class="kw">element_line</span>(<span class="dt">color =</span> <span class="st">&quot;gray90&quot;</span>),</span>
<span id="cb2-26"><a href="#cb2-26"></a>        <span class="dt">legend.position =</span> <span class="st">&quot;top&quot;</span>,</span>
<span id="cb2-27"><a href="#cb2-27"></a>        <span class="dt">plot.background =</span> <span class="kw">element_rect</span>(<span class="dt">fill =</span> <span class="st">&quot;white&quot;</span>, <span class="dt">color =</span> <span class="ot">NA</span>)</span>
<span id="cb2-28"><a href="#cb2-28"></a>        )  </span></code></pre></div>
<div class="figure" style="text-align: center">
<img src="data:image/png;base64,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" alt="Pilares en Comunidades Autonomas" width="100%" />
<p class="caption">
Pilares en Comunidades Autonomas
</p>
</div>
<div class="sourceCode" id="cb3"><pre class="sourceCode r"><code class="sourceCode r"><span id="cb3-1"><a href="#cb3-1"></a>spain_communities <span class="op">%&gt;%</span><span class="st"> </span></span>
<span id="cb3-2"><a href="#cb3-2"></a><span class="st">  </span><span class="kw">ggplot</span>() <span class="op">+</span><span class="st"> </span></span>
<span id="cb3-3"><a href="#cb3-3"></a><span class="st">  </span><span class="kw">geom_sf</span>() <span class="op">+</span><span class="st"> </span></span>
<span id="cb3-4"><a href="#cb3-4"></a><span class="st">  </span><span class="kw">geom_sf</span>(<span class="kw">aes</span>(<span class="dt">fill =</span> index_act), <span class="dt">show.legend =</span> F) <span class="op">+</span><span class="st">   </span></span>
<span id="cb3-5"><a href="#cb3-5"></a><span class="st">  </span><span class="kw">scale_fill_viridis_c</span>(<span class="dt">option =</span> <span class="st">&quot;plasma&quot;</span>,</span>
<span id="cb3-6"><a href="#cb3-6"></a>                       <span class="dt">breaks=</span><span class="kw">c</span>(<span class="dv">0</span>,.<span class="dv">25</span>,.<span class="dv">50</span>,.<span class="dv">75</span>,<span class="dv">1</span>)) <span class="op">+</span></span>
<span id="cb3-7"><a href="#cb3-7"></a><span class="st">  </span><span class="kw">geom_label</span>(<span class="kw">aes</span>(X, Y, <span class="dt">label =</span> NAME_<span class="dv">1</span>, <span class="dt">color =</span> index_act), </span>
<span id="cb3-8"><a href="#cb3-8"></a>             <span class="dt">size =</span> <span class="dv">3</span>, </span>
<span id="cb3-9"><a href="#cb3-9"></a>             <span class="dt">fontface =</span> <span class="st">&quot;bold&quot;</span>,</span>
<span id="cb3-10"><a href="#cb3-10"></a>             <span class="dt">show.legend =</span> F) <span class="op">+</span></span>
<span id="cb3-11"><a href="#cb3-11"></a><span class="st">  </span><span class="kw">scale_color_viridis_c</span>(<span class="dt">option =</span> <span class="st">&quot;plasma&quot;</span>) <span class="op">+</span></span>
<span id="cb3-12"><a href="#cb3-12"></a><span class="st">  </span><span class="kw">coord_sf</span>(<span class="dt">xlim =</span> <span class="kw">c</span>(<span class="op">-</span><span class="dv">19</span>, <span class="dv">-13</span>),</span>
<span id="cb3-13"><a href="#cb3-13"></a>           <span class="dt">ylim =</span> <span class="kw">c</span>(<span class="dv">27</span>, <span class="dv">30</span>),</span>
<span id="cb3-14"><a href="#cb3-14"></a>           <span class="dt">expand =</span> <span class="ot">FALSE</span>) <span class="op">+</span></span>
<span id="cb3-15"><a href="#cb3-15"></a><span class="st">  </span><span class="kw">theme_void</span>() <span class="op">+</span></span>
<span id="cb3-16"><a href="#cb3-16"></a><span class="st">  </span><span class="kw">theme</span>(<span class="dt">plot.background =</span> <span class="kw">element_rect</span>(<span class="dt">fill =</span> <span class="st">&quot;aliceblue&quot;</span>)) -&gt;<span class="st"> </span>sub_map1</span>
<span id="cb3-17"><a href="#cb3-17"></a></span>
<span id="cb3-18"><a href="#cb3-18"></a>world <span class="op">%&gt;%</span><span class="st"> </span></span>
<span id="cb3-19"><a href="#cb3-19"></a><span class="st">  </span><span class="kw">ggplot</span>() <span class="op">+</span><span class="st"> </span></span>
<span id="cb3-20"><a href="#cb3-20"></a><span class="st">  </span><span class="kw">geom_sf</span>(<span class="dt">color =</span> <span class="ot">NA</span>, <span class="dt">fill =</span> <span class="st">&quot;antiquewhite&quot;</span>) <span class="op">+</span></span>
<span id="cb3-21"><a href="#cb3-21"></a><span class="st">  </span><span class="kw">geom_sf</span>(<span class="dt">data =</span> spain_communities,</span>
<span id="cb3-22"><a href="#cb3-22"></a>          <span class="kw">aes</span>(<span class="dt">fill =</span> index_act)) <span class="op">+</span></span>
<span id="cb3-23"><a href="#cb3-23"></a><span class="st">  </span><span class="kw">scale_fill_viridis_c</span>(<span class="dt">option =</span> <span class="st">&quot;plasma&quot;</span>,</span>
<span id="cb3-24"><a href="#cb3-24"></a>                       <span class="dt">breaks=</span><span class="kw">c</span>(<span class="dv">0</span>,.<span class="dv">25</span>,.<span class="dv">50</span>,.<span class="dv">75</span>,<span class="dv">1</span>)) <span class="op">+</span></span>
<span id="cb3-25"><a href="#cb3-25"></a><span class="st">    </span><span class="kw">coord_sf</span>(<span class="dt">xlim =</span> <span class="kw">c</span>(<span class="op">-</span><span class="dv">10</span>, <span class="dv">5</span>),</span>
<span id="cb3-26"><a href="#cb3-26"></a>           <span class="dt">ylim =</span> <span class="kw">c</span>(<span class="dv">35</span>, <span class="dv">45</span>),</span>
<span id="cb3-27"><a href="#cb3-27"></a>           <span class="dt">expand =</span> <span class="ot">FALSE</span>) <span class="op">+</span></span>
<span id="cb3-28"><a href="#cb3-28"></a><span class="st">  </span><span class="kw">geom_label</span>(<span class="dt">data =</span> spain_communities, </span>
<span id="cb3-29"><a href="#cb3-29"></a>             <span class="kw">aes</span>(X, Y, <span class="dt">label =</span> NAME_<span class="dv">1</span>, <span class="dt">color =</span> index_act), </span>
<span id="cb3-30"><a href="#cb3-30"></a>             <span class="dt">size =</span> <span class="dv">3</span>, </span>
<span id="cb3-31"><a href="#cb3-31"></a>             <span class="dt">fontface =</span> <span class="st">&quot;bold&quot;</span>,</span>
<span id="cb3-32"><a href="#cb3-32"></a>             <span class="dt">show.legend =</span> F) <span class="op">+</span></span>
<span id="cb3-33"><a href="#cb3-33"></a><span class="st">  </span><span class="kw">scale_color_viridis_c</span>(<span class="dt">option =</span> <span class="st">&quot;plasma&quot;</span>) <span class="op">+</span></span>
<span id="cb3-34"><a href="#cb3-34"></a><span class="st">  </span><span class="kw">annotation_custom</span>(</span>
<span id="cb3-35"><a href="#cb3-35"></a>    <span class="dt">grob =</span> <span class="kw">ggplotGrob</span>(sub_map1),</span>
<span id="cb3-36"><a href="#cb3-36"></a>    <span class="dt">xmin =</span> <span class="dv">0</span>,</span>
<span id="cb3-37"><a href="#cb3-37"></a>    <span class="dt">xmax =</span> <span class="dv">4</span>,</span>
<span id="cb3-38"><a href="#cb3-38"></a>    <span class="dt">ymin =</span> <span class="dv">35</span>,</span>
<span id="cb3-39"><a href="#cb3-39"></a>    <span class="dt">ymax =</span> <span class="dv">37</span>) <span class="op">+</span></span>
<span id="cb3-40"><a href="#cb3-40"></a><span class="st">  </span><span class="kw">theme_void</span>() <span class="op">+</span></span>
<span id="cb3-41"><a href="#cb3-41"></a><span class="st">  </span><span class="kw">labs</span>(<span class="dt">fill =</span> <span class="st">&quot;Indice: </span><span class="ch">\n</span><span class="st">&quot;</span>,</span>
<span id="cb3-42"><a href="#cb3-42"></a>       <span class="dt">title =</span> <span class="st">&quot;Índice de Transparencia en Residencias de Mayores&quot;</span>,</span>
<span id="cb3-43"><a href="#cb3-43"></a>       <span class="dt">subtitle =</span> <span class="kw">sprintf</span>(<span class="st">&quot;Promedio: %s, Rango: 0 - 1&quot;</span>, <span class="kw">round</span>(<span class="kw">mean</span>(df<span class="op">$</span>index_act), <span class="dt">digits =</span> <span class="dv">2</span>)),</span>
<span id="cb3-44"><a href="#cb3-44"></a>       <span class="dt">caption =</span> <span class="st">&quot;Fuente: Perez-Duran &amp; Hernandez-Sanchez (2021)&quot;</span>) <span class="op">+</span></span>
<span id="cb3-45"><a href="#cb3-45"></a><span class="st">  </span><span class="kw">theme</span>(<span class="dt">legend.position =</span> <span class="st">&quot;bottom&quot;</span>, </span>
<span id="cb3-46"><a href="#cb3-46"></a>        <span class="dt">legend.key.width=</span> <span class="kw">unit</span>(<span class="dv">1</span>, <span class="st">&#39;cm&#39;</span>),</span>
<span id="cb3-47"><a href="#cb3-47"></a>        <span class="dt">legend.key.height =</span> <span class="kw">unit</span>(.<span class="dv">2</span>, <span class="st">&#39;cm&#39;</span>),</span>
<span id="cb3-48"><a href="#cb3-48"></a>        <span class="dt">legend.text =</span> <span class="kw">element_text</span>(<span class="dt">size =</span> <span class="dv">7</span>),</span>
<span id="cb3-49"><a href="#cb3-49"></a>        <span class="dt">panel.grid.major =</span> <span class="kw">element_line</span>(<span class="dt">color =</span> <span class="kw">gray</span>(.<span class="dv">8</span>), <span class="dt">linetype =</span> <span class="st">&quot;dashed&quot;</span>, <span class="dt">size =</span> <span class="fl">0.3</span>),</span>
<span id="cb3-50"><a href="#cb3-50"></a>        <span class="dt">panel.background =</span> <span class="kw">element_rect</span>(<span class="dt">fill =</span> <span class="st">&quot;aliceblue&quot;</span>, <span class="dt">color =</span> <span class="ot">NA</span>),</span>
<span id="cb3-51"><a href="#cb3-51"></a>        <span class="dt">plot.background =</span> <span class="kw">element_rect</span>(<span class="dt">fill =</span> <span class="st">&quot;white&quot;</span>, <span class="dt">color =</span> <span class="ot">NA</span>)</span>
<span id="cb3-52"><a href="#cb3-52"></a>        )  </span></code></pre></div>
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
<script>
$(document).ready(function () {
  window.initializeCodeFolding("show" === "show");
});
</script>


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
