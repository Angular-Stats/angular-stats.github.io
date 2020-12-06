---
layout: default
---
While Angular is one of the most famous frontend framework there are very few informations about its usage. This page tries to overcome this void and deliver reliable informations about hundred Angular projects hosted on GitHub and awarded with the most stars. There are only projects included which use angular-core as its dependency.

This is a part time project of mine. As I'm working as a Frontend Freelancer I often get questions about various usage of Angular so I started this research. If you want to get in touch with me, feel free to visit my [main page](https://patalas.github.io).

Last update: 05.12.2020

## Angular Core Version
@angular/core in dependencies
<canvas id="core"></canvas>
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
    var chart = new Chart('core', {
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
                return '' + args.value + '%';
              },
              position: 'outside'
            },
            {
            render: function (args) {
                return args.label;
              },
            fontColor: ['white', 'white', 'white', 'white']
            }
      ]              
    }
    }});
};
</script>
## File types
<canvas id="versions"></canvas>
<script>
d3.csv('/assets/stats/filetypes.csv')
  .then(makeFileTypesChart);

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

function makeFileTypesChart(data) {
    var dataLabels = data.map(function(d) {return d.Filetype});
    var dataValues = data.map(function(d) {return d.Percentage});
    var chart = new Chart('versions', {
        type: 'doughnut',
        data: {
            labels: dataLabels,
            datasets: [
              {
                  data: dataValues,
                          backgroundColor: [
                            "#3e95cd", "#8e5ea2","#3cba9f","#c45850", "#e8c3b9","#f38b4a"
        ],
              }
            ]
        },

     options: {
    plugins: {
      labels: [
            {
              render: function (args) {
                return '' + Math.round(args.value * 10000)/100 + '%';
              },
              position: 'outside'
            },
            {
            render: function (args) {
                return args.label;
              },
            fontColor: ['white', 'white', 'white', 'white']
            }
      ]              
    }
    }});
};
</script>
<!-- 
bundler exec jekyll build
bundler exec jekyll serve
-->