---
layout: default
---
While Angular is one of the most famous frontend framework there are very few informations about its usage. This page tries to overcome this void and deliver reliable informations about hundred Angular 2+ projects hosted on GitHub and awarded with the most stars. There are only projects included which use angular-core as its dependency.

This is a part time project of mine. As I'm working as a Frontend Freelancer I often get questions about various usage of Angular so I started this research. If you want to get in touch with me, feel free to visit my [main page](https://patalas.github.io).

Last update: 05.12.2020

### Angular Core Version
Only half of the projects are on major version 11 or 10. Suprisingly over 10% of the projects are on Version 6 or older.
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
              textMargin: 8,
              render: function (args) {
                return args.value + '%';
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
### File types
It's not a big suprise that half of the files are typescript files. 
<canvas id="filetypes"></canvas>
<script>
d3.csv('/assets/stats/filetypes.csv')
  .then(makeFileTypesChart);

function makeFileTypesChart(data) {
    var dataLabels = data.map(function(d) {return d.Filetype});
    var dataValues = data.map(function(d) {return d.Percentage});
    var chart = new Chart('filetypes', {
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
              textMargin: 8,
              render: function (args) {
                return Math.round(args.value * 10000)/100 + '%';
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
### Size of the projects
<canvas id="files"></canvas>
<script>
d3.csv('/assets/stats/files.csv')
  .then(makeChart);

function makeChart(data) {
    var dataLabels = data.map(function(d) {return d.Size});
    var dataValues = data.map(function(d) {return d.Number});
    var chart = new Chart('files', {
        type: 'bar',
        data: {
            labels: dataLabels,
            datasets: [
            {
                data: dataValues,
                backgroundColor: ["#3e95cd", "#8e5ea2","#3cba9f","#c45850", "#e8c3b9","#f38b4a"]
            }
            ]
        },
         options: {
           plugins: { labels: { render: function (args) { return args.value + "%" } } },
          
      legend: { display: false },
       title: {
        display: true,
        text: "Number of files except files and folders starting with a dot"
      }}});
};
</script>
<!-- 
bundler exec jekyll build
bundler exec jekyll serve
-->