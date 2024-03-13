<script>
  import { onMount } from 'svelte';
  import echarts from 'echarts';
  
  let myChart;

  onMount(() => {
    myChart = echarts.init(document.getElementById('main'));

    const mapData = [
      { name: '北京', value: 100 },
      { name: '上海', value: 200 },
      // 其他省份数据
    ];

    const option = {
      tooltip: {
        trigger: 'item',
        formatter: '{b}：{c}'
      },
      visualMap: {
        min: 0,
        max: 1000,
        left: 'left',
        top: 'bottom',
        text: ['高', '低'],
        calculable: true
      },
      series: [
        {
          name: '数据名称',
          type: 'map',
          map: 'china',
          roam: true,
          label: {
            show: true
          },
          data: mapData
        }
      ]
    };

    myChart.setOption(option);

    // 添加事件监听器
    myChart.on('click', function (params) {
      console.log(params.name); // 输出点击的省份名称
      console.log(params.value); // 输出点击的省份数据值
    });
  });
</script>

<div id="main" style="width: 600px; height: 400px;"></div>