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

<!-- <div id="chart-container" >
  <SvelteFC {...chartConfig} />
</div> -->