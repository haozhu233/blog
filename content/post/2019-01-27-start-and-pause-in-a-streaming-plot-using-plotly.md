---
title: Start and Pause in a Streaming Plot using plotly
author: Hao
date: '2019-01-27'
slug: start-and-pause-in-a-streaming-plot-using-plotly
categories:
- R
tags:
- R
- tutorial
---
 
[plotly](https://plot.ly) has [a very nice example](https://plot.ly/r/streaming/) about how to making a streaming plot in R. When I was working on the `arduino` package, I need this feature because I want to create a plotting panel where data will be plotted once collected. So I used that example and quickly created a streaming app. 

Here is the core part from the example

```r
p <- plot_ly(
  y = c(rand(),rand(),rand()),
  type = 'scatter',
  mode = 'lines',
  line = list(
    color = '#25FEFD',
    width = 3
    )
  ) %>%
  layout(yaxis = list(range = c(0,10)))

output$plot <- renderPlotly(p)

observeEvent(input$button, {
  while(TRUE){
    Sys.sleep(1)
    plotlyProxy("plot", session) %>%
    plotlyProxyInvoke("extendTraces", list(y=list(list(rand()))), list(0))
  }
})
```
(For the complete example, check out the original link.)

So basically this is done by creating a shiny app and use `plotlyProxyInvoke` to send additional data through the `extendTraces` track to a named plotly plot called "plot". I'm very satisfied with the result. 

However, I quickly run into a problem that I don't know how to pause this streaming without stopping this app. Below is my first attempt.

```r
observeEvent(input$start, {
    rv$state <- 1 - rv$state
    while(rv$state == 1){
    Sys.sleep(1)
    plotlyProxy("plot", session) %>%
    plotlyProxyInvoke("extendTraces", list(y=list(list(rand()))), list(0))
  }
  })
```

Here, I created a `reactiveValue` in shiny and was hoping it could help me to controll the `while` loop. I mean, in theory, this mechanism looks like it will work, right? However, it turned out that I was underestimating the power of `while`. When we use to `while` or `repeat` to get the streaming feature, this iteration process completely blocks the current R thread, which was also used by the shiny app. In this case, there is no way for the shiny app to move around during the looping. One obvious solution is to create a child thread here but do we really need to get that complicated?

All of a sudden, I recalled a magical command in Shiny that [Joe](https://twitter.com/jcheng) talked about during useR! 2016: [`invalidateLater()`](https://shiny.rstudio.com/reference/shiny/0.14/invalidateLater.html). This command "schedules the current reactive context to be invalidated in the given number of milliseconds.". What does it mean? It will force a reactive object to be re-evaluated after a certain period of time. This is exactly what I need! So I made some modifacations to the previous code.

```r
observeEvent(input$start, {
    rv$state <- 1 - rv$state
})

observe({
  invalidateLater(1)
  if (rv$state == 1) {
    Sys.sleep(1)
    plotlyProxy("plot", session) %>%
    plotlyProxyInvoke("extendTraces", list(y=list(list(rand()))), list(0))
  }
})
```

So, in the real example, I got

<iframe width="560" height="315" src="https://www.youtube.com/embed/C6mvf5CKX-c" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

I can't expect more!

You can find the real example in the `arduino` package. 