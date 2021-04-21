<script>
  import FusionCharts from 'fusioncharts';
  import Widgets from 'fusioncharts/fusioncharts.widgets';
  import FusionTheme from 'fusioncharts/themes/fusioncharts.theme.fusion';
  import SvelteFC, { fcRoot } from 'svelte-fusioncharts';
  import dataSource from './risparmio.js';

  fcRoot(FusionCharts, Widgets, FusionTheme);

  let chartConfig = {
      type: 'angulargauge',
      width: '100%',
      height: '400',
      renderAt: 'chart-container',
      dataSource
  };
</script>

<div id="chart-container" >
  <SvelteFC {...chartConfig} />
</div>
<!-- <script>
    import FusionCharts from 'fusioncharts';
    import Widgets from 'fusioncharts/fusioncharts.widgets';
    import FusionTheme from 'fusioncharts/themes/fusioncharts.theme.fusion';
    import SvelteFC, { fcRoot } from 'svelte-fusioncharts';
    import dataSource from './risparmio.js';
  
    fcRoot(FusionCharts, Widgets, FusionTheme);
  
    let chartConfig = {
        type: 'angulargauge',
        width: '100%',
        height: '400',
        renderAt: 'chart-container',
        dataSource
    };
</script>
  
<div id="chart-container" >
    <SvelteFC {...chartConfig} />
</div> -->

<!-- <script>
    import FusionCharts from 'fusioncharts';
    import Charts from 'fusioncharts/fusioncharts.charts';
    import FusionTheme from 'fusioncharts/themes/fusioncharts.theme.fusion';
    import SvelteFC, { fcRoot } from 'svelte-fusioncharts';

    import dataApp from '../data.js';

    import Api from '../Api.js';

    let chartConfig
    let dataSource
    
    let entrate = []
    let data = []

    onMount(async () => {
		    const response = await Api.get('/movement/findAll')

        entrate = response.result.filter(movimento => {
            if (movimento.type === "entrata") {
                return movimento
            }
        })

        for (let categoria of dataApp.categorieEntrate) {
          var totalamount = 0
          for (let entrata of entrate) {
              if (entrata.category === categoria) {
                totalamount += entrata.amount
              }
          }
          if (totalamount > 0) {
            data.push({"label": categoria.toString(), "value": totalamount.toString()})
          }
        }

        dataSource = {
            "chart": {
                "caption": "Break-up of Annual Revenue",
                "subcaption": "In Million $",
                "xaxisname": "Year",
                "yaxisname": "Sales in M$",
                "numberprefix": "$",
                "numbersuffix": "M",
                "showsum": "1",
                "plottooltext": "Revenue from <b>$seriesName</b> in $label was <b>$dataValue</b>",
                "theme": "fusion"
            },
            "categories": [
                {
                "category": [
                    {
                    "label": "Entrate"
                    },
                    {
                    "label": "Uscite"
                    }
                ]
            }
          ]
        }
            ]
        }

    
  
    fcRoot(FusionCharts, Charts, FusionTheme);
  
    chartConfig = {
      type: 'doughnut2d',
      width: '100%',
      height: '400',
      renderAt: 'chart-container',
      dataSource
    };

    });
    
    // Always set FusionCharts as the first parameter
    fcRoot(FusionCharts, Charts, FusionTheme);
    
    const dataSource = {
      "chart": {
        "caption": "Yearly Energy Production Rate",
        "subcaption": " Top 5 Developed Countries",
        "numbersuffix": " TWh",
        "showsum": "1",
        "plottooltext": "$label produces <b>$dataValue</b> of energy from $seriesName",
        "theme": "fusion",
        "drawcrossline": "1"
      },
      "categories": [
        {
          "category": [
            {
              "label": "Entrate"
            },
            {
              "label": "Uscite"
            },
            {
              "label": "Russia"
            },
            {
              "label": "Australia"
            },
            {
              "label": "United States"
            },
            {
              "label": "France"
            }
          ]
        }
      ],
      "dataset": [
        {
          "seriesname": "Coal",
          "data": [
            {
              "value": "400"
            },
            {
              "value": "830"
            },
            {
              "value": "500"
            },
            {
              "value": "420"
            },
            {
              "value": "790"
            },
            {
              "value": "380"
            }
          ]
        },
        {
          "seriesname": "Hydro",
          "data": [
            {
              "value": "350"
            },
            {
              "value": "620"
            },
            {
              "value": "410"
            },
            {
              "value": "370"
            },
            {
              "value": "720"
            },
            {
              "value": "310"
            }
          ]
        },
        {
          "seriesname": "Nuclear",
          "data": [
            {
              "value": "210"
            },
            {
              "value": "400"
            },
            {
              "value": "450"
            },
            {
              "value": "180"
            },
            {
              "value": "570"
            },
            {
              "value": "270"
            }
          ]
        },
        {
          "seriesname": "Gas",
          "data": [
            {
              "value": "180"
            },
            {
              "value": "330"
            },
            {
              "value": "230"
            },
            {
              "value": "160"
            },
            {
              "value": "440"
            },
            {
              "value": "350"
            }
          ]
        },
        {
          "seriesname": "Oil",
          "data": [
            {
              "value": "60"
            },
            {
              "value": "200"
            },
            {
              "value": "200"
            },
            {
              "value": "50"
            },
            {
              "value": "230"
            },
            {
              "value": "150"
            }
          ]
        }
      ]
    };
    
    const chartConfigs = {
       type: 'stackedcolumn2d',
       width: '100%',
       height: '400',
       dataFormat: 'json',
       dataSource
    };
    </script>
    
    <SvelteFC {...chartConfigs} /> -->