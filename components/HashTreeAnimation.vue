<script setup>
import { onMounted } from 'vue'
import * as d3 from 'd3'

onMounted(() => {
  const svg = d3.select('#hash-anim')
    .append('svg')
    .attr('width', 600)
    .attr('height', 400)

  const loop = () => {
    svg.selectAll('*').remove()

    // Query Point
    const query = svg.append('circle')
      .attr('cx', 100)
      .attr('cy', 200)
      .attr('r', 8)
      .attr('fill', 'orange')
      .attr('opacity', 0)

    svg.append('text')
      .attr('x', 80)
      .attr('y', 190)
      .text('Query')
      .attr('fill', 'white')
      .attr('opacity', 0)
      .transition().delay(200).duration(300).attr('opacity', 1)

    query.transition()
      .delay(500)
      .duration(500)
      .attr('opacity', 1)

    const comparePoints = d3.range(5).map((_, i) => ({
      x: 160 + i * 30,
      y: 160 + (i % 2 === 0 ? -20 : 20)
    }))

    setTimeout(() => {
      svg.selectAll('.compare')
        .data(comparePoints)
        .enter()
        .append('circle')
        .attr('class', 'compare')
        .attr('cx', d => d.x)
        .attr('cy', d => d.y)
        .attr('r', 0)
        .attr('fill', 'lightblue')
        .transition()
        .duration(500)
        .attr('r', 6)

      svg.append('text')
        .attr('x', 200)
        .attr('y', 120)
        .text('Comparison Set (C)')
        .attr('fill', 'white')
        .attr('opacity', 0)
        .transition().delay(200).duration(300).attr('opacity', 1)
    }, 1000)

    // Arrow to tree
    setTimeout(() => {
      svg.append('line')
        .attr('x1', 130)
        .attr('y1', 200)
        .attr('x2', 130)
        .attr('y2', 200)
        .attr('stroke', 'white')
        .attr('stroke-width', 2)
        .transition()
        .duration(800)
        .attr('x2', 400)
        .attr('y2', 200)
    }, 1800)

    const treeBranches = [
      { x1: 400, y1: 200, x2: 450, y2: 150 },
      { x1: 400, y1: 200, x2: 450, y2: 250 },
      { x1: 450, y1: 150, x2: 500, y2: 130 },
      { x1: 450, y1: 150, x2: 500, y2: 170 },
      { x1: 450, y1: 250, x2: 500, y2: 230 },
      { x1: 450, y1: 250, x2: 500, y2: 270 }
    ]

    setTimeout(() => {
      svg.selectAll('.branch')
        .data(treeBranches)
        .enter()
        .append('line')
        .attr('class', 'branch')
        .attr('x1', d => d.x1)
        .attr('y1', d => d.y1)
        .attr('x2', d => d.x1)
        .attr('y2', d => d.y1)
        .attr('stroke', '#888')
        .attr('stroke-width', 2)
        .transition()
        .duration(600)
        .attr('x2', d => d.x2)
        .attr('y2', d => d.y2)

      svg.append('text')
        .attr('x', 420)
        .attr('y', 110)
        .text('Hash Tree')
        .attr('fill', 'white')
        .attr('opacity', 0)
        .transition().duration(300).attr('opacity', 1)
    }, 2800)

    setTimeout(() => {
      svg.selectAll('.branch')
        .transition()
        .duration(600)
        .attr('stroke', (d, i) => i % 2 === 0 ? 'limegreen' : '#444')
    }, 3600)

    // Loop every 6s
    setTimeout(loop, 3000)
  }

  loop()
})
</script>

<template>
  <div id="hash-anim" class="w-full h-full flex justify-center items-center"></div>
</template>

<style scoped>
#hash-anim svg {
  background-color: #1a1a1a;
  border-radius: 8px;
}
</style>