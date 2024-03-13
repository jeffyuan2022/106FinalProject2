<script>
    import { onMount } from 'svelte';
    import { fade } from 'svelte/transition';
    // import 'daisyui/dist/full.css';
    import * as echarts from 'echarts';
    let isVisible = false;

    let chart;

    async function renderChart() {
      const chartContainer = document.getElementById('chart-container-1');

      if (!chart) {
        chart = echarts.init(chartContainer);
      }
      let dataAxis = ['点', '击', '柱', '子', '或', '者', '两', '指', '在', '触', '屏', '上', '滑', '动', '能', '够', '自', '动', '缩', '放'];
      // prettier-ignore
      let data = [220, 182, 191, 234, 290, 330, 310, 123, 442, 321, 90, 149, 210, 122, 133, 334, 198, 123, 125, 220];
      let yMax = 500;
      let dataShadow = [];
      for (let i = 0; i < data.length; i++) {
        dataShadow.push(yMax);
      }
      const options = {
        title: {
          text: '特性示例：渐变色 阴影 点击缩放',
          subtext: 'Feature Sample: Gradient Color, Shadow, Click Zoom',
          show: false
        },
        grid: {
          top: '-20px', // 调整这里可以实现图表整体上移
          bottom: '10%',
          left: '20px', // 设置为 0%
          right: '0%', // 设置为 0%
          containLabel: true
        },        
        xAxis: {
          data: dataAxis,
          axisLabel: {
            inside: true,
            color: '#fff'
          },
          axisTick: {
            show: false
          },
          axisLine: {
            show: false
          },
          z: 10
        },
        yAxis: {
          axisLine: {
            show: false
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            color: '#999'
          }
        },
        dataZoom: [
          {
            type: 'inside'
          }
        ],
        series: [
          {
            type: 'bar',
            showBackground: true,
            itemStyle: {
              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                { offset: 0, color: '#83bff6' },
                { offset: 0.5, color: '#188df0' },
                { offset: 1, color: '#188df0' }
              ])
            },
            emphasis: {
              itemStyle: {
                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  { offset: 0, color: '#2378f7' },
                  { offset: 0.7, color: '#2378f7' },
                  { offset: 1, color: '#83bff6' }
                ])
              }
            },
            data: data
          }
        ]  
      };

      chart.setOption(options);
    }  
    onMount(() => {
      renderChart();
    });
  </script>
  <div class="box">
    <div class="introduction">
      <h1 style="font-weight: 600;margin-bottom: 15px;">Exploring the Impact of Wage Disparities</h1>
      <ul>
          <li>What are the primary factors driving wage disparities?</li>
          <li>How significant are these disparities across different sectors and demographics?</li>
          <li>What are some less obvious influences that contribute to wage disparities?</li>
          <li>Why is addressing wage disparities important for economic, social, and policy-making contexts?</li> 
          <li>How significant are these disparities across different sectors and demographics?sectors</li>   
          <li>What are some less obvious influences that contribute to wage disparities?</li>       
      </ul>
    </div>
    <div id="chart-container-1" style="width: 60%; height: 400px;"></div>
  </div>


  
  <style>
    .box{
      width: 100%;
      height: 400px;
    }
    .introduction {
      width: 40%;
      padding: 20px;
      background-color: #f3f3f3;
      border-radius: 8px;
      margin-bottom: 20px;
      font-family: Arial, sans-serif;
      color: #333;
      line-height: 1.6;
      text-align: center;
      float: left;
    }
    #chart-container-1{
      float: left;
      width: 60%;
    }
  </style>
  