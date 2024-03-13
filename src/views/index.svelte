<script>
    import { fade } from 'svelte/transition'; // 导入渐隐过渡
    import L1_Intro from './font/L1_Intro.svelte';
    import L2_IncomeGap from './font/L2_IncomeGap.svelte';
    import L3_Bread from './font/L3_Bread.svelte';
    import L4_IntroEdu from './font/L4_IntroEdu.svelte';
    import L5_EduGap from './font/L5_EduGap.svelte'; 
    import L6_ExpEdu from './font/L6_ExpEdu.svelte';
    import L7_AfterEdu from './font/L7_AfterEdu.svelte'; 
    import L8_AgeEdu from './font/L8_AgeEdu.svelte';  
    import L9_LogAge from './font/L9_LogAge.svelte';  
    import L10_Region from './font/L10_Region.svelte';  
    import L11_Conclusion from './font/L11_Conclusion.svelte'; 

    import R1_Intro from './charts/R1_Intro.svelte';
    import R2_IncomeGap from './charts/R2_IncomeGap.svelte';
    import R3_Bread from './charts/R3_Bread.svelte';
    import R4_IntroEdu from './charts/R4_IntroEdu.svelte';
    import R5_EduGap from './charts/R5_EduGap.svelte'; 
    import R6_ExpEdu from './charts/R6_ExpEdu.svelte';
    import R7_AfterEdu from './charts/R7_AfterEdu.svelte';
    import R8_AgeEdu from './charts/R8_AgeEdu.svelte';   
    import R9_LogAge from './charts/R9_LogAge.svelte';    
    import R10_Region from './charts/R10_Region.svelte';   
    import R11_Conclusion from './charts/R11_Conclusion.svelte'; 
    
    
    let items = [
        {
            id: 0,
            code: 'item0'
        },
        {
            id: 1,
            code: 'item1'
        },
        {
            id: 2,
            code: 'item2'
        },
        {
            id: 3,
            code: 'item3'
        },
        {
            id: 4,
            code: 'item4'
        },    
        {
            id: 5,
            code: 'item5'
        },    
        {
            id: 6,
            code: 'item6'
        },    
        {
            id: 7,
            code: 'item7'
        },
        {
            id: 8,
            code: 'item8'
        },    
        {
            id: 9,
            code: 'item9'
        },
        {
            id: 10,
            code: 'item10'
        },
        {
            id: 11,
            code: 'item11'
        }                               
    ];
    const components = [
        { name: 'L1_Intro', component: L1_Intro },
        { name: 'L2_IncomeGap', component: L2_IncomeGap },
        { name: 'L3_Bread', component: L3_Bread },
        { name: 'L4_IntroEdu', component: L4_IntroEdu },
        { name: 'L5_EduGap', component: L5_EduGap },
        { name: 'L6_ExpEdu', component: L6_ExpEdu },
        { name: 'L7_AfterEdu', component: L7_AfterEdu },
        { name: 'L8_AgeEdu', component: L8_AgeEdu },
        { name: 'L9_LogAge', component: L9_LogAge },
        { name: 'L10_Region', component: L10_Region },
        { name: 'L11_Conclusion', component: L11_Conclusion }             
    ];
    const charts = [
        { name: 'R1_Intro', component: R1_Intro },
        { name: 'R2_IncomeGap', component: R2_IncomeGap },
        { name: 'R3_Bread', component: R3_Bread },
        { name: 'R4_IntroEdu', component: R4_IntroEdu },
        { name: 'R5_EduGap', component: R5_EduGap },
        { name: 'R6_ExpEdu', component: R6_ExpEdu },
        { name: 'R7_AfterEdu', component: R7_AfterEdu },
        { name: 'R8_AgeEdu', component: R8_AgeEdu },
        { name: 'R9_LogAge', component: R9_LogAge },
        { name: 'R10_Region', component: R10_Region },
        { name: 'R11_Conclusion', component: R11_Conclusion }
    ];    
    let selectedContent = '';
    let selectedContentId = 0;
    function selectItem(index) {
      selectedContent = items[index].code;
      selectedContentId = items[index].id;
    }
  
    function handleScroll(event) {
      const scrollPosition = event.target.scrollTop + 350;
      const index = Math.floor(scrollPosition / 450); // 假设每个项的高度为400px
      selectedContent = items[index].code;
      selectedContentId = items[index].id;
    }
  </script>
  
  
  <div class="container">
    <div class="left-panel" on:scroll={handleScroll}>
      {#each items as item, index}
        <div  class="item {selectedContentId === index ? '' : 'selected'}" on:click={() => selectItem(index)}>          
          {#if components[index]}
            <svelte:component this={components[index].component} />
          {/if}
        </div>
      {/each}
    </div>
    <div>
      <!-- {selectedContent} -->
      {#each items as item, index}
        <div class="right-panel">
          {#if selectedContentId===null}
            <L1_Intro/>
          {/if}  
          {#if charts[selectedContentId]}
            <svelte:component this={charts[selectedContentId].component} />
          {/if}        
        </div>
      {/each}      
    </div>
  </div>
  <style>
    .container {
      display: flex;
      width: 100%;
      height: 100%;
    }
  
    .left-panel {
      overflow-y: auto;
      width: 50%;
      padding: 20px 10px;
      margin-left: 3%;
      margin: 100px 0;
      margin-top: 100px;
      margin-left: -20%;
    }
    .item {
      width: 100%;
      padding: 10px;
      cursor: pointer;
      height: 400px;
      margin: 10px 0;    
    }
  
    .right-panel {
      padding: 20px;
      width: 45%;
      height: 500px;
      position: fixed;
      left: 45%;
      top: 15%;
      overflow: auto;
    }
    ::-webkit-scrollbar {
	  width: 0px;
	  border-radius: 0rem;
	  height: 0px;
	}
    /* 定义渐隐动画 */
    @keyframes fadeOut {
        from {
          opacity: 1; /* 初始透明度为 1 */
        }
        to {
          opacity: 0; /* 结束透明度为 0 */
        }
    }

    /* 应用渐隐动画 */
    .item.selected {
        animation: fadeOut 1.5s ease forwards; /* 持续时间为 0.5 秒，渐变效果为 ease，并保持动画结束状态 */
        animation-delay: 0.2s; /* 设置延迟为 0.2 秒 */
    }
  </style>

