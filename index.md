---
layout: default
---
While Angular is one of the most famous frontend framework there are very few informations about its usage. This page tries to overcome this void and deliver reliable informations about hundred Angular projects hosted on GitHub and awarded with the most stars. There are only projects included which use angular-core as its dependency.

This is a part time project of mine. As I'm working as a Frontend Freelancer I often get questions about various usage of Angular so I started this research. If you want to get in touch with me, feel free to visit my [main page](https://patalas.github.io).

Last update: 05.12.2020

## Angular Core Version

<canvas id="chart"></canvas>
<script>

d3.csv('/assets/stats/versions.csv')
  .then(makeChart);

var greenToRedColors = [
"#ff3366",
"#ff6633",
"#FFCC33",
"#33FF66",
"#33FFCC",
"#33CCFF",
"#3366FF",
"#6633FF",
"#CC33FF"
];



function makeChart(data) {
    var dataLabels = data.map(function(d) {return d.Version});
    var dataValues = data.map(function(d) {return d.Number});
    var colors = data.map(function(d) { return greenToRedColors[d.Version - 3]});
    var chart = new Chart('chart', {
        type: 'doughnut',
        data: {
            labels: dataLabels,
            datasets: [
            {
                data: dataValues,
                backgroundColor: colors
            }
            ]
        },
     options: {
    plugins: {
      labels: [
            {
                render: function (args) {
      return '' + args.label + '';
    },
            position: 'outside'
            },
            {
            render: 'percentage',
            fontColor: ['white', 'white', 'white', 'white']
            }
      ]              
    }
    }});
};
</script>