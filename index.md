---
layout: default
---
While Angular is one of the most well-known frontend frameworks, there is very little information available about its use. This page seeks to fill this void and provide reliable statistics based on the 100 Angular 2+ repositories that have been awarded the most stars and are hosted on GitHub.

We only included repositories which use angular-core as its dependency. This statistics was created in December 2020. We used the master branch of each repository for this analysis. At the end you find a [list of all repositories](#list-of-all-repositories) which were evaluated in this study. 

This is a part time project of mine. Since I work as a front-end freelancer, I often get questions about the various uses of Angular, so I started this research. If you want to get in touch with me, please visit my [main page](https://patalas.github.io).

### Angular Core Version
On of the most interesting question was on which major version most of the repositories are. Even though it breaks our story telling, we would like to start with it. Suprisingly only half of the repositories are on major version 11 or 10. We had suspect a much higher percentage. What was shocking to us was the 11% with Version 6 or lower.  Version 6 was realeased in May 2018, Version 5 and 4 November respectively March 2017.
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

### Abandoned repositories
After seeing so many repositories still on core versions older than two or more years, we asked ourselves, if there are abandoned repositories. For each repository we determine the last commit date, which should be a good indication, if this repository is still in development. We checked if the last commit date is fresh (younger than a month), half fresh (between one and three months), oldie (three to six months) or rotten (older than six months). To get a better feeling with our predictions related to the used core version, we split the repositories in these using Angular 11/10 and all others with Angular 9 or older.

<canvas id="abandoned"></canvas>
<script>
d3.csv('/assets/stats/active.csv')
  .then(makeChart);

function makeChart(data) {
    var dataLabels = data.map(function(d) {return d.Range});
    var dataValues1 = data.map(function(d) {return d.Number1});
    var dataValues2 = data.map(function(d) {return d.Number2});
    var colors = data.map(function(d) { return greenToRedColors[d.Version - 3]});
    var chart = new Chart('abandoned', {
        type: 'bar',
        data: {
            labels: dataLabels,
            datasets: [
            {
                label: 'With Angular 9 or older',
                data: dataValues1,
                backgroundColor: "#c45850"
            }, {
                label: 'With Angular 11/10',
                data: dataValues2,
                backgroundColor: "#3cba9f"
            }
            ]
        },
         options: {
           plugins: { labels: { render: function (args) { return args.value } } },
          
      legend: { display: true },
        title: {
        display: true,
        text: "Last commit older than x months"
      }
      }});
};
</script>
Our presumption seems to be right. Nearly half of the repositories with Angular 9 or older seems to be abandoned (last commit older than half a year). But there are still fresh repositories, who doesn't jump to the latest Angular version. There is still more research to do. We don't want to go any further and take a look at other aspects.
### GitHub Commits per Year
The number of the commits per year shows us a good picture of the activity inside the repositories. We see a steady grow up to 2017 with a big jump 2018, following by a weak 2019 and 2020. We don't have enough inside data to give a reason for the fall.  
<canvas id="log-years"  style="margin-bottom: 5rem"></canvas>
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


### Size of the Projects
After getting a first inside about the repositories we are facing, we wanted to know more about their structure. We started to get a look on the size of the repositories. We thought about to count all files, but that is very misleading. A small repositories with few functionality but a lot of pictures would look enormous. We decided to count only this filetypes: ts, js, json, scss, css, sass, less and htm/html. Additionally we excluded all folder and files starting with a dot.
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
        text: "Number of files (ts, js, json, scss, css, sass, less and htm/html)"
      }}});
};
</script>
One third of the repositories are in the category 20-50, something we expected. Whats rather interesting is that over 20% of the repositories are rather big with over 200 files.
### File types
It's not a big suprise that half of the files are typescript files. What is interesting, that with scss on the third place, most projects seems to favour Scss over the other options.
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






<div style="margin-top: 10rem"></div>

### List of all repositories
This is the list of all one hundred evaluated repositories for this study. To get this list, we get a list of over 200 Angular tagged repositories with the most stars given in GitHub. After that we removed all repositories, which do not use the @angular-core dependency. This are most likely repositories, which are related to Angular, like for example the Angular project itself, but they do not use Angular. For the remaining we took the first one hundred with the most stars, which are listed below. 
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