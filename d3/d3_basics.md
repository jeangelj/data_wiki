##data join
    var any_variable_name_you_can_think_of = d3.select("body").selectAll("g")
          .data(parts)
        .enter()
          .append("g")
          .text(function(d) { return d; });
