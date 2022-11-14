---
title: Marginal Effects and Stargazer
subtitle: This tutorial shows how to put margins output into a stargazer table

# Summary for listings and search engines
summary: This tutorial shows how to put margins output into a stargazer table.

# Image
image:
  caption: 'Image credit: [**Unsplash/Lazarescu Alexandra**](https://unsplash.com/photos/kxFBzUtLx00)'
  focal_point: ""
  preview_only: false
  
# Link this post with a project
projects: []

# Date published
date: "2022-11-14T00:00:00Z"

# Date updated
lastmod: "2022-11-14T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

authors:
- admin

tags:
- R
- margins
- stargazer

categories:
- Tutorial
- Regression Analysis
- Data Visualization
---

</head>

<body>


<div class="container-fluid main-container">




<div id="header">



<h1 class="title toc-ignore">Marginal Effects and Stargazer</h1>
<h4 class="author">Alfredo Hernandez Sanchez</h4>
<h4 class="date">2022-11-14</h4>

</div>


<div id="the-problem" class="section level2">
<h2>The Problem</h2>
<p>Though the <code>stargazer</code> package is widely used and an
excellent and flexible way of creating tables with different model
classes. It does not integrate output from the, equally popular, margins
package.</p>
<pre class="r"><code>library(tidyverse) # for %&gt;% 
library(margins) # for marginal effects
library(AER) # for HMDA data
library(DescTools) # for McFadden&#39;s R2
library(stargazer) # for tables</code></pre>
<p>Let´s use the Home Mortgage Disclosure Act Data from the
<code>AER</code> package as an example. Here we try to predict if a
mortgage was denied.</p>
<pre class="r"><code># Read Data on Denial of Mortgages 
data(HMDA)

# Transform Data to Numeric (for LPM)
df &lt;- HMDA %&gt;% 
  mutate(deny = ifelse(deny == &quot;no&quot;, 0, 1))</code></pre>
<p>First let’s explore the relationship between mortgage denial
<code>deny</code> and Payments to income ratio <code>pirat</code>.</p>
<p><img src="data:image/png;base64,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" width="672" /></p>
<p>Next, let’s run some models.</p>
<pre class="r"><code># Linear Probability Model
lpm &lt;- lm(deny ~ pirat + hschool + afam, 
         data = df)

# Logit Link Model
logit &lt;- glm(deny ~ pirat + hschool + afam,
         data = df, 
         family = &quot;binomial&quot;)

# Probit Link Model
probit &lt;- glm(deny ~ pirat + hschool + afam,
        data = df, 
        family = binomial(link = &quot;probit&quot;))</code></pre>
<p>We can contrast all of them in a table using the stargazer
package.</p>
<pre class="r"><code>stargazer(lpm, probit, logit,
          type = &quot;html&quot;)</code></pre>
<table style="text-align:center">
<tr>
<td colspan="4" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td colspan="3">
<em>Dependent variable:</em>
</td>
</tr>
<tr>
<td>
</td>
<td colspan="3" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td colspan="3">
deny
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
<em>OLS</em>
</td>
<td>
<em>probit</em>
</td>
<td>
<em>logistic</em>
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(1)
</td>
<td>
(2)
</td>
<td>
(3)
</td>
</tr>
<tr>
<td colspan="4" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
pirat
</td>
<td>
0.549<sup>***</sup>
</td>
<td>
2.743<sup>***</sup>
</td>
<td>
5.365<sup>***</sup>
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(0.060)
</td>
<td>
(0.381)
</td>
<td>
(0.728)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
hschoolyes
</td>
<td>
-0.097<sup>*</sup>
</td>
<td>
-0.468<sup>**</sup>
</td>
<td>
-0.805<sup>**</sup>
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(0.051)
</td>
<td>
(0.229)
</td>
<td>
(0.399)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
afamyes
</td>
<td>
0.176<sup>***</sup>
</td>
<td>
0.701<sup>***</sup>
</td>
<td>
1.258<sup>***</sup>
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(0.018)
</td>
<td>
(0.084)
</td>
<td>
(0.147)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
Constant
</td>
<td>
0.009
</td>
<td>
-1.800<sup>***</sup>
</td>
<td>
-3.333<sup>***</sup>
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(0.056)
</td>
<td>
(0.263)
</td>
<td>
(0.471)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td colspan="4" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
Observations
</td>
<td>
2,380
</td>
<td>
2,380
</td>
<td>
2,380
</td>
</tr>
<tr>
<td style="text-align:left">
R<sup>2</sup>
</td>
<td>
0.077
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
Adjusted R<sup>2</sup>
</td>
<td>
0.076
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
Log Likelihood
</td>
<td>
</td>
<td>
-795.139
</td>
<td>
-793.868
</td>
</tr>
<tr>
<td style="text-align:left">
Akaike Inf. Crit.
</td>
<td>
</td>
<td>
1,598.277
</td>
<td>
1,595.737
</td>
</tr>
<tr>
<td style="text-align:left">
Residual Std. Error
</td>
<td>
0.312 (df = 2376)
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
F Statistic
</td>
<td>
66.481<sup>***</sup> (df = 3; 2376)
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td colspan="4" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
<em>Note:</em>
</td>
<td colspan="3" style="text-align:right">
<sup><em></sup>p&lt;0.1; <sup><strong></sup>p&lt;0.05;
<sup></strong></em></sup>p&lt;0.01
</td>
</tr>
</table>
<p>Now let’s get the marginal effects (AME) of the <code>probit</code>
model.</p>
<pre class="r"><code>summary(margins(probit))</code></pre>
<pre><code>##      factor     AME     SE       z      p   lower  upper
##     afamyes  0.1671 0.0242  6.9135 0.0000  0.1197 0.2145
##  hschoolyes -0.1077 0.0636 -1.6918 0.0907 -0.2324 0.0171
##       pirat  0.5002 0.0688  7.2686 0.0000  0.3653 0.6351</code></pre>
</div>
<div id="a-not-so-elegant-solution" class="section level2">
<h2>A (not so elegant) solution</h2>
<p>We can impute the AME coefficients to the original model object
<code>probit</code>.</p>
<pre class="r"><code>probit -&gt; old_model

if(old_model$family$link %in% c(&quot;logit&quot;, &quot;probit&quot;)){
  # The package that is needed
  require(margins)
  # Some redundancy (just in case you run twice!)
  new_model &lt;- old_model
  # Extract the margins coefficients (named numeric array)
  marginal_coefficients &lt;- summary(margins(old_model))$AME
  # Match margins coefficients to model object by (variable) name
  for(i in names(marginal_coefficients)) {
    new_model$coefficients[[i]] &lt;- marginal_coefficients[[i]]
  }
  # If the model is neither probit nor logit
} else {print(&quot;Invalid Model&quot;)}

probit_margins &lt;- new_model</code></pre>
<pre class="r"><code>summary(probit_margins)</code></pre>
<pre><code>## 
## Call:
## glm(formula = deny ~ pirat + hschool + afam, family = binomial(link = &quot;probit&quot;), 
##     data = df)
## 
## Deviance Residuals: 
##     Min       1Q   Median       3Q      Max  
## -2.1145  -0.4772  -0.4253  -0.3518   2.8879  
## 
## Coefficients:
##             Estimate Std. Error z value Pr(&gt;|z|)    
## (Intercept) -1.79983    0.26291  -6.846  7.6e-12 ***
## pirat        0.50021    0.38051   1.315   0.1886    
## hschoolyes  -0.10765    0.22942  -0.469   0.6389    
## afamyes      0.16709    0.08355   2.000   0.0455 *  
## ---
## Signif. codes:  0 &#39;***&#39; 0.001 &#39;**&#39; 0.01 &#39;*&#39; 0.05 &#39;.&#39; 0.1 &#39; &#39; 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 1744.2  on 2379  degrees of freedom
## Residual deviance: 1590.3  on 2376  degrees of freedom
## AIC: 1598.3
## 
## Number of Fisher Scoring iterations: 5</code></pre>
<p>Unfortunately, our standard errors have not been updated! We can
extract them into a separate object.</p>
<pre class="r"><code>se_probit &lt;- summary(margins(probit))$SE
names(se_probit) &lt;- str_remove_all(names(se_probit), &quot;Var_dydx_&quot;)
se_probit</code></pre>
<pre><code>##    afamyes hschoolyes      pirat 
## 0.02416841 0.06363396 0.06881847</code></pre>
<pre class="r"><code># List of Custom Standard Errors (for stargazer)
custom_se &lt;- list(sqrt(diag(vcov(lpm))),
                  se_probit)</code></pre>
<p>Let´s also add McFadden’s pseudo R2.</p>
<pre class="r"><code>PseudoR2(probit,&quot;McFaddenAdj&quot;)</code></pre>
<pre><code>## McFaddenAdj 
##  0.08364626</code></pre>
<pre class="r"><code># Custom list of Adj. R2 for stargazer
custom_r2 = list(c(&quot;McFadden Adj. R Sq.&quot;, 
                 &quot;&quot;,
                 round(PseudoR2(probit,&quot;McFaddenAdj&quot;),digits = 2)
))</code></pre>
</div>
<div id="the-result" class="section level2">
<h2>The Result</h2>
<p>Now we can create a table which compares both models using
stargazer!</p>
<pre class="r"><code># Our Comparative Table
stargazer(lpm, probit_margins,
          type = &quot;html&quot;,
          # Our custom r2
          add.lines = custom_r2,
          # Our custom standard errors
          se = custom_se)</code></pre>
<table style="text-align:center">
<tr>
<td colspan="3" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td colspan="2">
<em>Dependent variable:</em>
</td>
</tr>
<tr>
<td>
</td>
<td colspan="2" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td colspan="2">
deny
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
<em>OLS</em>
</td>
<td>
<em>probit</em>
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(1)
</td>
<td>
(2)
</td>
</tr>
<tr>
<td colspan="3" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
pirat
</td>
<td>
0.549<sup>***</sup>
</td>
<td>
0.500<sup>***</sup>
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(0.060)
</td>
<td>
(0.069)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
hschoolyes
</td>
<td>
-0.097<sup>*</sup>
</td>
<td>
-0.108<sup>*</sup>
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(0.051)
</td>
<td>
(0.064)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
afamyes
</td>
<td>
0.176<sup>***</sup>
</td>
<td>
0.167<sup>***</sup>
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(0.018)
</td>
<td>
(0.024)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
Constant
</td>
<td>
0.009
</td>
<td>
-1.800
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(0.056)
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td colspan="3" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
McFadden Adj. R Sq.
</td>
<td>
</td>
<td>
0.08
</td>
</tr>
<tr>
<td style="text-align:left">
Observations
</td>
<td>
2,380
</td>
<td>
2,380
</td>
</tr>
<tr>
<td style="text-align:left">
R<sup>2</sup>
</td>
<td>
0.077
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
Adjusted R<sup>2</sup>
</td>
<td>
0.076
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
Log Likelihood
</td>
<td>
</td>
<td>
-795.139
</td>
</tr>
<tr>
<td style="text-align:left">
Akaike Inf. Crit.
</td>
<td>
</td>
<td>
1,598.277
</td>
</tr>
<tr>
<td style="text-align:left">
Residual Std. Error
</td>
<td>
0.312 (df = 2376)
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
F Statistic
</td>
<td>
66.481<sup>***</sup> (df = 3; 2376)
</td>
<td>
</td>
</tr>
<tr>
<td colspan="3" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
<em>Note:</em>
</td>
<td colspan="2" style="text-align:right">
<sup><em></sup>p&lt;0.1; <sup><strong></sup>p&lt;0.05;
<sup></strong></em></sup>p&lt;0.01
</td>
</tr>
</table>
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
