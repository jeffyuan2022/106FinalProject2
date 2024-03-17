<script>
  // You can also define the URL dynamically in the script tag
  let websiteUrl = 'https://www.youtube.com/watch?v=kpD3i3RNhc4';
  function handleClick(event) {
    // Prevent default link behavior
    event.preventDefault();
    
    // Log click or perform other actions
    console.log('Link clicked!');

    // Navigate to the URL
    window.location.href = websiteUrl;
  }
</script>

<div class="video">
  <a href={websiteUrl} on:click={handleClick}>YouTube Demo Video</a>
</div>
<div class="fontBox">
  <h1 class="fontBox_1">How Does the Return on Education Influence Wage Disparities Across Different Demographics</h1>
  <div class="fontBox_2">
    <h3 class="fontBox_2">Wage disparities represent a significant challenge that intersects with economic equity, social justice, and policy development. These disparities not only reflect but also contribute to the inequalities within our societies, impacting millions of lives by influencing access to resources, opportunities, and wellbeing.</h3>
  </div>
  <div class="fontBox_3">
    Author: Andrew Zhao, Yiheng Yuan
  </div>
  <div class="scroll-message-container">
    <div class="scroll-arrow">
      ↓
    </div>
    <p class="scroll-text">Scroll down at the left center to start to explore</p>
  </div>

</div>
<style>
  .fontBox{
    padding: 20px 0;
  }
  .fontBox_1{
    font-weight: 600;
    font-size: 45px;
  }
  .fontBox_2{
    font-weight: 200;
    font-size: 20px;
  }
  .fontBox_3{
    font-size: 20px;
    color: red;
  }
  .scroll-message-container {
    position: absolute; /* or absolute, depending on your layout */
    bottom: 20px; /* Adjust as needed */
    left: 15%; /* Center horizontally */
    transform: translateX(-50%);
    display: flex;
    align-items: center;
    justify-content: center;
    animation: bounce 2s infinite; /* Animation for the arrow */
    cursor: pointer; /* Optional, if you want to make it clickable */
  }
  .video {
    position: absolute; /* or absolute, depending on your layout */
    top: 50px; /* Adjust as needed */
    left: 50%; /* Center horizontally */
    transform: translateX(-50%);
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer; /* Optional, if you want to make it clickable */
    font-size: 24px;
  }

  .scroll-arrow {
    font-size: 30px; /* Adjust size as needed */
    margin-right: 10px; /* Space between arrow and text */
  }

  .scroll-text {
    font-size: 24px; /* Adjust size as needed */
    color: #000000; /* Adjust color as needed */
  }

  @keyframes bounce {
    0%, 20%, 50%, 80%, 100% {
      transform: translateY(0);
    }
    40% {
      transform: translateY(-20px);
    }
    60% {
      transform: translateY(-10px);
    }
  }
</style>
