<template>
    <div>
        <svg id='viz' width='600' height='400'></svg>
    </div>
</template>

<script>
    const d3 = require('d3');

    function BarChart() {
        let barColor = "orange";
        const scaleLength = d3.scaleLinear().domain([0, 40]).range([0, 200]);
        const scaleY = d3
            .scaleBand()
            .domain(d3.range(10))
            .range([0, 300])
            .paddingInner(0.05);

        function my(selection) {
            const myData = selection.datum();
            scaleY.domain(d3.range(myData.length));

            const gs = selection
                .selectAll("g")
                .data(myData)
                .join("g")
                .attr("transform", (d, i) => `translate(${10},${scaleY(i)})`);

            gs.selectAll("rect")
                .data((d) => [d])
                .join("rect")
                .attr("height", scaleY.bandwidth())
                .attr("width", scaleLength)
                .attr("fill", barColor);

            gs.selectAll("text")
                .data((d) => [d])
                .join("text")
                .attr("dx", 5)
                .attr("y", scaleY.bandwidth())
                .attr("dy", -3)
                .text((d) => d);
        }

        my.barColor = function (value) {
            if (!arguments.length) return barColor;
            barColor = value;
            return my;
        };

        return my;
    }

    export default {
        name: "BarChartVisualizer",
        props:{
            numbers: Array,
        },
        data: function(){
            return {
                barChart: BarChart().barColor('orange'),
            }
        },
        watch:{
           numbers: function(newValue){
               d3.select("#viz").datum(newValue).call(this.barChart);
           }
        }
    }
</script>

<style scoped>

</style>