<script>
    import { onMount } from 'svelte';
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
            "showpercentvalues": "0",
            "showlabels": "0",
            "showvalues": "0",
            "defaultcenterlabel": "Entrate",
            "aligncaptionwithcanvas": "0",
            "captionpadding": "0",
            "decimals": "1",
            "plottooltext": "<b>$percentValue $label</b>",
            "centerlabel": "$value €",
            "theme": "fusion"
          },
          "data": data
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

</script>

<div id="chart-container" >
    <SvelteFC {...chartConfig} />
</div>