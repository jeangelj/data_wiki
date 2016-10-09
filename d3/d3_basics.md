##d3 basic commands

d3 or var (add explanation when to use which)

        .select() //
        .selectAll() //
        .append() //
        .attr() //
        .style() //
        .data() //
        .enter() // 

##data join
    var any_variable_name_you_can_think_of = d3.select("body").selectAll("g")
          .data(parts)
        .enter()
          .append("g")
          .text(function(d) { return d; });
          
##margins

    var margin = {top: 20, right: 60, bottom: 60, left: 20};
    var width = 800 - margin.left - margin.right,
        height = 500 - margin.top - margin.bottom;

    var svg = d3.select("body").append("svg")
        .attr("width", width + margin.left + margin.right)
        .attr("height", height + margin.top + margin.bottom)
      .append("g")
        .attr("transform", "translate(" + margin.left + "," + margin.top + ")");


##scales

    .scale.linear()
    .domain()
    .range()
    //hard-code or 
    .set()
    .extent()
    .min()
    .max()

##axes 

    var xAxis = d3.axisBottom(xScale)
    .tickSize(-height);
    
    var yAxis = d3.axisRight(yScale)
    .tickSize(-width)
    .tickFormat(d3.format("$,"));

##classes

    .classed()
    .attr("class","dots")

##transition 

    .transition() // 
    .duration() // 
