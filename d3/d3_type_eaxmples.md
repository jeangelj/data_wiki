## bar chart 

## path 
    
    //line generator
    var incomeLine = d3.line()
        .curve(d3.curveCardinal)
        .x(function(d) { return xScale(d.year); })
        .y(function(d) { return yScale(d.val); });
    
    //create the path
    svg.append("path")
      .datum(usData[0].values)
      .attr("class", "incomeLine")
      .attr("d", incomeLine);

## chord `  
