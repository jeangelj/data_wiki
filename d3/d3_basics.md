## data selection 

        d3.selectAll("p")
            .attr("class", "graph")
            .style("color", "blue");
    
is the same as 

        var p = d3.selectAll("p");
            p.attr("class", "graf");
            p.style("color", "red");
            
d3 selects the first element that matches the specified selector string; while using var selects the local variable 

##d3 basic commands

        .select() // select & return one element
        .selectAll() // select and return all found elements 
        .append() // create a new element inside the selection 
        .attr() // add HTML attributes to the selection 
        .style() // add CSS style to selection 

##data join

        .data() // bind an array of data to selection
        .enter() // return selection of “new placeholder" elements

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
    
##functions

        //d = use "anonymous" functions to access data or values bound to elements
        d3.selectAll("rect")
                .attr("height",	function(d){
                 return	d.value; //Set the height to 'value'
                 });
                 
        d3.selectAll("rect")
                .attr("x",function(d,i)	{return	i*10;//	Move each rect to the right}
                );

##Notes

- as a best practice, finish each statement with ";"
