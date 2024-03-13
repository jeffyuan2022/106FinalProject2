<script>
    import { onMount } from 'svelte';
    // import 'daisyui/dist/full.css';
    import * as echarts from 'echarts';

    let chart;

    async function renderChart() {
      const chartContainer = document.getElementById('chart-container-line-1');

      if (!chart) {
        chart = echarts.init(chartContainer);
      }
      // prettier-ignore
      let data = [220, 182, 191, 234, 290, 330, 310, 123, 442, 321, 90, 149, 210, 122, 133, 334, 198, 123, 125, 220];
      const options = {
        title: {
          text: '可滑动折线图--2',
          // subtext: 'Feature Sample: Gradient Color, Shadow, Click Zoom',
          top:'0'
        },
        grid: {
          top: '0%', // 调整这里可以实现图表整体上移
          bottom: '0%',
          left: '0%', // 设置为 0%
          right: '0%', // 设置为 0%
          containLabel: true
        },           
        toolbox: {
          show: true,
          feature: {
            mark: { show: true },
            dataView: { show: true, readOnly: false },
            magicType: { show: true, type: ['line', 'bar'] },
            restore: { show: true },
            saveAsImage: { show: true }
          }
        },
        calculable: true,
        legend: {
          data: ['Budget 2011'],
          itemGap: 5
        },
        grid: {
          top: '12%',
          left: '1%',
          right: '10%',
          containLabel: true
        },
        xAxis: [
          {
            type: 'category',
            data: data
          }
        ],
        yAxis: [
          {
            type: 'value',
            name: '数值',
          }
        ],
        dataZoom: [
          {
            show: true,
            start: -100,
            end: 100
          },
          {
            type: 'inside',
            start: -100,
            end: 100
          },
        ],
        series: [
          {
            name: 'Budget 2011',
            type: 'line',
            data: data
          },
        ]        
      };

      chart.setOption(options);
      window.addEventListener('resize', function () {
        chart.resize();
      });          
    }  
    onMount(() => {
      renderChart();
    });
  </script>
  <div class="box">
    <div id="chart-container-line-1"></div>
  </div>


  
  <style>
    .box{
      width: 100%;
      height: 600px;
      padding: 20px 0;
    }
    #chart-container-line-1{
      width: 100%;
      height: 85%;
    }
  </style>
  