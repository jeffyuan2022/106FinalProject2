<script>
  import { onMount } from 'svelte';
  import * as d3 from 'd3';

  let loavesCount = 2322;
  let svg;

  onMount(() => {
    const iconWidth = 30;
    const iconHeight = 30;
    const margin = { top: 10, right: 10, bottom: 10, left: 10 };
    const iconsPerRow = Math.floor(window.innerWidth / iconWidth);
    const numRows = Math.ceil(loavesCount / iconsPerRow);
    const svgWidth = iconsPerRow * iconWidth + margin.left + margin.right;
    const svgHeight = numRows * iconHeight + margin.top + margin.bottom;

    const container = d3.select(svg)
      .attr('viewBox', `0 0 ${svgWidth} ${svgHeight}`)
      .attr('preserveAspectRatio', 'xMidYMid meet');

    const loavesData = Array.from({ length: loavesCount }, (_, i) => ({
      id: i,
      x: (i % iconsPerRow) * iconWidth + margin.left,
      y: Math.floor(i / iconsPerRow) * iconHeight + margin.top,
    }));

    // Animation for bread icons
    container.selectAll('image')
      .data(loavesData)
      .enter()
      .append('image')
      .attr('xlink:href', './bread_1.png')
      .attr('width', iconWidth)
      .attr('height', iconHeight)
      .attr('x', d => d.x)
      .attr('y', d => d.y)
      .attr('opacity', 0)
      .transition()
      .delay((_, i) => i * 2) // Adjust delay for faster animation
      .duration(0) // Duration of fade-in for each icon
      .attr('opacity', 1);

    // Display text and shade after all animations have finished
    setTimeout(() => {
      // Calculate center and dimensions for the text and its background
      const centerTextX = svgWidth / 2;
      const centerTextY = svgHeight / 2 - 100;
      const textPadding = 240;
      const rectHeight = 80;

      // Append semi-transparent rectangle for text background
      container.append('rect')
        .attr('x', centerTextX - 500 - textPadding)
        .attr('y', centerTextY + 175 - textPadding)
        .attr('width', 1000 + (textPadding * 2))
        .attr('height', rectHeight)
        .attr('fill', 'white')
        .attr('opacity', 0.7);

      // Append text messages
      const textMessage = "That's nearly 2,322 loaves of bread!";
      const textLoaves = ``;

      container.append('text')
        .attr('x', centerTextX)
        .attr('y', centerTextY)
        .attr('text-anchor', 'middle')
        .style('font-size', '96px')
        .style('font-weight', 'bold')
        .text(textMessage);

      container.append('text')
        .attr('x', centerTextX)
        .attr('y', centerTextY + 30) // Position below the first text element
        .attr('text-anchor', 'middle')
        .style('font-size', '24px')
        .style('font-weight', 'bold')
        .text(textLoaves);

    }, loavesData.length * 2 + 10); // Calculate based on the last bread animation
  });
</script>

<svg bind:this={svg} style="width: 100%; height: auto;"></svg>
