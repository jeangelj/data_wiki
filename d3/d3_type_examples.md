## bar chart 

## dot plot

    svg.selectAll("circle")
        .data(myDataset)
        .enter().append("circle")
        .attr("cx", function(d) { return xScale(d.x); })
        .attr("cy", function(d) { return yScale(d.y); })
        .attr("r", 5);

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
