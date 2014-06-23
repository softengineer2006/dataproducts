---
title       : BMI Calculator
subtitle    : Slidify Project
author      : Memon Adnan Akbar
job         : Team Lead
framework   : io2012   # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
ext_widgets : {rCharts: ["libraries/highcharts", "libraries/nvd3", "libraries/morris"]} 
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Presentation Scheme

1. What is BMI?
2. BMI Calculation
3. BMI Ranges

--- .class #id

## Body Mass Index (BMI)

1. The body mass index (BMI), or Quetelet index, is a measure of relative weight based on an individual's mass and height
2. Devised between 1830 and 1850 by the Belgian polymath Adolphe Quetelet
3. It is a simple method to assess how much an individual's body weight departs from what is normal or desirable for a person of his or her height

---

## BMI Calculation

<img height='450' src='formula.png' />

---

## BMI Ranges



<div id = 'chart3' class = 'rChart nvd3'></div>
<script type='text/javascript'>
 $(document).ready(function(){
      drawchart3()
    });
    function drawchart3(){  
      var opts = {
 "dom": "chart3",
"width":    800,
"height":    400,
"x": "criteria",
"y": "index",
"group": "group",
"type": "multiBarChart",
"id": "chart3" 
},
        data = [
 {
 "criteria": "BMI",
"index":             18,
"group": "under-weight" 
},
{
 "criteria": "BMI",
"index":            0.5,
"group": "thin-for-height" 
},
{
 "criteria": "BMI",
"index":            6.4,
"group": "healthy-weight" 
},
{
 "criteria": "BMI",
"index":              5,
"group": "over-weight" 
} 
]
  
      if(!(opts.type==="pieChart" || opts.type==="sparklinePlus" || opts.type==="bulletChart")) {
        var data = d3.nest()
          .key(function(d){
            //return opts.group === undefined ? 'main' : d[opts.group]
            //instead of main would think a better default is opts.x
            return opts.group === undefined ? opts.y : d[opts.group];
          })
          .entries(data);
      }
      
      if (opts.disabled != undefined){
        data.map(function(d, i){
          d.disabled = opts.disabled[i]
        })
      }
      
      nv.addGraph(function() {
        var chart = nv.models[opts.type]()
          .width(opts.width)
          .height(opts.height)
          
        if (opts.type != "bulletChart"){
          chart
            .x(function(d) { return d[opts.x] })
            .y(function(d) { return d[opts.y] })
        }
          
         
        chart
  .stacked(true)
          
        

        
        
        
      
       d3.select("#" + opts.id)
        .append('svg')
        .datum(data)
        .transition().duration(500)
        .call(chart);

       nv.utils.windowResize(chart.update);
       return chart;
      });
    };
</script>
---




