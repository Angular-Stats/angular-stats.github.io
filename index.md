---
layout: default
---
While Angular is one of the most famous frontend framework there are very few informations about its usage. This page tries to overcome this void and deliver reliable informations about hundred Angular 2+ projects hosted on GitHub and awarded with the most stars. There are only projects included which use angular-core as its dependency.

This is a part time project of mine. As I'm working as a Frontend Freelancer I often get questions about various usage of Angular so I started this research. If you want to get in touch with me, feel free to visit my [main page](https://patalas.github.io).

This statistics was created on December 2020. At the end you find a [list of all projects](#list-of-all-projects-evaluated-for-this-study) which were evaluated in this study. 

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

### GitHub Commits per Year
<canvas id="log-years"></canvas>

<script>
d3.csv('/assets/stats/log-years.csv')
  .then(makeChartLogYears);

function makeChartLogYears(data) {
    var dataLabels = data.map(function(d) {return d.Year});
    var dataValues = data.map(function(d) {return d.Number});
    var chart = new Chart('log-years', {
        type: 'bar',
        data: {
            labels: dataLabels,
            datasets: [
            {
                data: dataValues,
                backgroundColor: ["#AA33FF","#447766","#3cba9f","#c45850", "#e8c3b9","#f38b4a", "#8e5ea2" , "#3e95cd"]
            }
            ]
        },
         options: {
           plugins: { labels: { render: function (args) { return "" } } },
          
      legend: { display: false },
       title: {
        display: true,
        text: "Number of commits per year"
      }}});
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

### Size of the Projects
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




<div style="margin-top: 20rem"></div>

### List of all projects evaluated for this study
- SortableJS/ngx-sortablejs <https://github.com/SortableJS/ngx-sortablejs>
- ngrx/example-app <https://github.com/ngrx/example-app>
- sweetalert2/ngx-sweetalert2 <https://github.com/sweetalert2/ngx-sweetalert2>
- NathanWalker/angular-seed-advanced <https://github.com/NathanWalker/angular-seed-advanced>
- po-ui/po-angular <https://github.com/po-ui/po-angular>
- aviabird/angularspree <https://github.com/aviabird/angularspree>
- KillerCodeMonkey/ngx-quill <https://github.com/KillerCodeMonkey/ngx-quill>
- SebastianM/angular-google-maps <https://github.com/SebastianM/angular-google-maps>
- DevCloudFE/ng-devui <https://github.com/DevCloudFE/ng-devui>
- akveo/nebular <https://github.com/akveo/nebular>
- microsoft/angular-react <https://github.com/microsoft/angular-react>
- xieziyu/ngx-echarts <https://github.com/xieziyu/ngx-echarts>
- seokju-na/geeks-diary <https://github.com/seokju-na/geeks-diary>
- amazon-archives/aws-cognito-angular-quickstart <https://github.com/amazon-archives/aws-cognito-angular-quickstart>
- swimlane/ngx-charts <https://github.com/swimlane/ngx-charts>
- qdouble/angular-webpack-starter <https://github.com/qdouble/angular-webpack-starter>
- ikismail/Angular-ShoppingCart <https://github.com/ikismail/Angular-ShoppingCart>
- mgechev/angular-seed <https://github.com/mgechev/angular-seed>
- tomastrajan/angular-ngrx-material-starter <https://github.com/tomastrajan/angular-ngrx-material-starter>
- ng-alain/ng-alain <https://github.com/ng-alain/ng-alain>
- alexjlockwood/ShapeShifter <https://github.com/alexjlockwood/ShapeShifter>
- damienbod/angular-auth-oidc-client <https://github.com/damienbod/angular-auth-oidc-client>
- AnthonyNahas/ngx-auth-firebaseui <https://github.com/AnthonyNahas/ngx-auth-firebaseui>
- avatsaev/angular-contacts-app-example <https://github.com/avatsaev/angular-contacts-app-example>
- rangle/augury <https://github.com/rangle/augury>
- angular/flex-layout <https://github.com/angular/flex-layout>
- ngx-formly/ngx-formly <https://github.com/ngx-formly/ngx-formly>
- mdbootstrap/Angular-Bootstrap-with-Material-Design <https://github.com/mdbootstrap/Angular-Bootstrap-with-Material-Design>
- cyrilletuzi/angular-async-local-storage <https://github.com/cyrilletuzi/angular-async-local-storage>
- bitwarden/web <https://github.com/bitwarden/web>
- cipchk/ngx-weui <https://github.com/cipchk/ngx-weui>
- AlexKhymenko/ngx-permissions <https://github.com/AlexKhymenko/ngx-permissions>
- ngneat/content-loader <https://github.com/ngneat/content-loader>
- ngrx/platform <https://github.com/ngrx/platform>
- ngx-translate/core <https://github.com/ngx-translate/core>
- ever-co/ever <https://github.com/ever-co/ever>
- aws-samples/aws-mobile-appsync-chat-starter-angular <https://github.com/aws-samples/aws-mobile-appsync-chat-starter-angular>
- guillotinaweb/ngx-schema-form <https://github.com/guillotinaweb/ngx-schema-form>
- mgechev/ngrev <https://github.com/mgechev/ngrev>
- DanielYKPan/date-time-picker <https://github.com/DanielYKPan/date-time-picker>
- Ricbet/panel-magic <https://github.com/Ricbet/panel-magic>
- udos86/ng-dynamic-forms <https://github.com/udos86/ng-dynamic-forms>
- maxisam/ngx-clipboard <https://github.com/maxisam/ngx-clipboard>
- bitwarden/browser <https://github.com/bitwarden/browser>
- wordpress-clients/hybrid <https://github.com/wordpress-clients/hybrid>
- swimlane/ngx-graph <https://github.com/swimlane/ngx-graph>
- r-park/todo-angular-firebase <https://github.com/r-park/todo-angular-firebase>
- CreativeIT/material-angular-dashboard <https://github.com/CreativeIT/material-angular-dashboard>
- TrilonIO/aspnetcore-angular-universal <https://github.com/TrilonIO/aspnetcore-angular-universal>
- jfcere/ngx-markdown <https://github.com/jfcere/ngx-markdown>
- auth0/angular2-jwt <https://github.com/auth0/angular2-jwt>
- DavideViolante/Angular-Full-Stack <https://github.com/DavideViolante/Angular-Full-Stack>
- stbui/angular-material-app <https://github.com/stbui/angular-material-app>
- housseindjirdeh/angular2-hn <https://github.com/housseindjirdeh/angular2-hn>
- juristr/angular-testing-recipes <https://github.com/juristr/angular-testing-recipes>
- angular/components <https://github.com/angular/components>
- JsDaddy/ngx-mask <https://github.com/JsDaddy/ngx-mask>
- MurhafSousli/ngx-progressbar <https://github.com/MurhafSousli/ngx-progressbar>
- naveedgol/music-web-player <https://github.com/naveedgol/music-web-player>
- swimlane/ngx-datatable <https://github.com/swimlane/ngx-datatable>
- mathisGarberg/angular-folder-structure <https://github.com/mathisGarberg/angular-folder-structure>
- ngneat/transloco <https://github.com/ngneat/transloco>
- IgniteUI/igniteui-angular <https://github.com/IgniteUI/igniteui-angular>
- stefanoslig/angular-ngrx-nx-realworld-example-app <https://github.com/stefanoslig/angular-ngrx-nx-realworld-example-app>
- zxing-js/ngx-scanner <https://github.com/zxing-js/ngx-scanner>
- ng-select/ng-select <https://github.com/ng-select/ng-select>
- ng-alain/delon <https://github.com/ng-alain/delon>
- orizens/echoes-player <https://github.com/orizens/echoes-player>
- linnovate/mean <https://github.com/linnovate/mean>
- trimox/angular-mdc-web <https://github.com/trimox/angular-mdc-web>
- bitwarden/desktop <https://github.com/bitwarden/desktop>
- ThorstenHans/ngx-electron <https://github.com/ThorstenHans/ngx-electron>
- mseemann/angular2-mdl <https://github.com/mseemann/angular2-mdl>
- kolkov/angular-editor <https://github.com/kolkov/angular-editor>
- MurhafSousli/ngx-sharebuttons <https://github.com/MurhafSousli/ngx-sharebuttons>
- Teradata/covalent <https://github.com/Teradata/covalent>
- angulartics/angulartics2 <https://github.com/angulartics/angulartics2>
- MurhafSousli/ngx-gallery <https://github.com/MurhafSousli/ngx-gallery>
- mgechev/codelyzer <https://github.com/mgechev/codelyzer>
- Angular-RU/universal-starter <https://github.com/Angular-RU/universal-starter>
- Kyusung4698/PoE-Overlay <https://github.com/Kyusung4698/PoE-Overlay>
- johnpapa/angular-ngrx-data <https://github.com/johnpapa/angular-ngrx-data>
- swimlane/ngx-ui <https://github.com/swimlane/ngx-ui>
- fulls1z3/universal <https://github.com/fulls1z3/universal>
- Ismaestro/angular9-example-app <https://github.com/Ismaestro/angular9-example-app>
- abacritt/angularx-social-login <https://github.com/abacritt/angularx-social-login>
- aitboudad/ngx-loading-bar <https://github.com/aitboudad/ngx-loading-bar>
- angular-split/angular-split <https://github.com/angular-split/angular-split>
- UltimateAngular/ngx-errors <https://github.com/UltimateAngular/ngx-errors>
- jiayihu/ng-animate <https://github.com/jiayihu/ng-animate>
- ng-matero/ng-matero <https://github.com/ng-matero/ng-matero>
- TwanoO67/bootstraping-ngx-admin-lte <https://github.com/TwanoO67/bootstraping-ngx-admin-lte>
- ng-lightning/ng-lightning <https://github.com/ng-lightning/ng-lightning>
- swimlane/ngx-dnd <https://github.com/swimlane/ngx-dnd>
- shlomiassaf/ngx-modialog <https://github.com/shlomiassaf/ngx-modialog>
- angular/angularfire <https://github.com/angular/angularfire>
- cedoor/mindmapp <https://github.com/cedoor/mindmapp>
- xmlking/ngx-starter-kit <https://github.com/xmlking/ngx-starter-kit>
- ngx-rocket/starter-kit <https://github.com/ngx-rocket/starter-kit>
- datorama/akita <https://github.com/datorama/akita>

<!-- 
bundler exec jekyll build
bundler exec jekyll serve
-->