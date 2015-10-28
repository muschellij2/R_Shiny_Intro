---
title: "R Shiny Intro Pres"
author: "John Muschelli"
date: '2015-10-28'
output: 
  ioslides_presentation:
    logo: logo.png
    incremental: true
runtime: shiny
---

## Shiny in R

- What is Shiny in R?

> - A web application framework for R
> - Turn your analyses into interactive web applications

- No HTML, CSS, or JavaScript knowledge required*
- (*Sort of)
- Go to the [Gallery](http://shiny.rstudio.com/gallery/)


## Default Interactive Plot

<!--html_preserve--><div class="shiny-input-panel">
<div class="shiny-flow-layout">
<div>
<div class="form-group shiny-input-container">
<label class="control-label" for="n_breaks">Number of bins:</label>
<div>
<select id="n_breaks"><option value="10">10</option>
<option value="20" selected>20</option>
<option value="35">35</option>
<option value="50">50</option></select>
<script type="application/json" data-for="n_breaks" data-nonempty="">{}</script>
</div>
</div>
</div>
<div>
<div class="form-group shiny-input-container">
<label class="control-label" for="bw_adjust">Bandwidth adjustment:</label>
<input class="js-range-slider" id="bw_adjust" data-min="0.2" data-max="2" data-from="1" data-step="0.2" data-grid="true" data-grid-num="9" data-grid-snap="false" data-prettify-separator="," data-keyboard="true" data-keyboard-step="11.1111111111111" data-drag-interval="true" data-data-type="number"/>
</div>
</div>
</div>
</div><!--/html_preserve--><!--html_preserve--><div id="out6dc710cb12040152" class="shiny-plot-output" style="width: 100% ; height: 400px"></div><!--/html_preserve-->


## Why Shiny?

- The user can INTERACT with the data and R
- Usually, only one of them is possible
- No Code - complete web app
- Can use all the things R has to offer


## Default Interactive Plot Input (UI) Code


```r
inputPanel(
  selectInput("n_breaks", label = "Number of bins:",
              choices = c(10, 20, 35, 50), selected = 20),
  
  sliderInput("bw_adjust", label = "Bandwidth adjustment:",
              min = 0.2, max = 2, value = 1, step = 0.2)
)
```


## Default Interactive Plot Output (Server) Code


```r
renderPlot({
  hist(faithful$eruptions, probability = TRUE, breaks = as.numeric(input$n_breaks),
       xlab = "Duration (minutes)", main = "Geyser eruption duration")
  
  dens <- density(faithful$eruptions, adjust = input$bw_adjust)
  lines(dens, col = "blue")
})
```



## Just quick table (ugly)


```r
summary(cars)
```

```
##      speed           dist       
##  Min.   : 4.0   Min.   :  2.00  
##  1st Qu.:12.0   1st Qu.: 26.00  
##  Median :15.0   Median : 36.00  
##  Mean   :15.4   Mean   : 42.98  
##  3rd Qu.:19.0   3rd Qu.: 56.00  
##  Max.   :25.0   Max.   :120.00
```

## Just quick table (less ugly, but still ugly)


```r
renderTable({
  summary(cars)
})
```

<!--html_preserve--><div id="outefa5971428b05beb" class="shiny-html-output"></div><!--/html_preserve-->

## Just quick table (less ugly, but still ugly)

Takes same arguments as `print.xtable`

```r
renderTable({
  summary(cars)
}, include.rownames = FALSE)
```

<!--html_preserve--><div id="outb699989bdd069b2b" class="shiny-html-output"></div><!--/html_preserve-->



## DataTables in Shiny

<!--html_preserve--><div id="out660a0a0adffecbe9" class="shiny-datatable-output"></div><!--/html_preserve-->

## DataTables in Shiny


```r
renderDataTable({
  cars
  })
```


