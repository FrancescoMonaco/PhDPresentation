<script setup>
import { ref, onMounted } from 'vue'
import * as d3 from 'd3'

const width = 800
const height = 400

onMounted(() => {
  const svg = d3.select('#hash-tree-svg')
    .append('svg')
    .attr('width', width)
    .attr('height', height)

  const query = svg.append('circle')
    .attr('cx', 50)
    .attr('cy', 200)
    .attr('r', 10)
    .attr('fill', 'orange')
    .attr('opacity', 0)

  const C = [0, 1, 2].map(i =>
    svg.append('circle')
      .attr('cx', 150)
      .attr('cy', 150 + i * 50)
      .attr('r', 10)
      .attr('fill', d3.schemeCategory10[i])
      .attr('opacity', 0)
  )

  const arrow = svg.append('line')
    .attr('x1', 200)
    .attr('y1', 200)
    .attr('x2', 200)
    .attr('y2', 200)
    .attr('stroke', 'black')
    .attr('marker-end', 'url(#arrow)')
    .attr('opacity', 0)

  // Define marker
  svg.append('defs').append('marker')
    .attr('id', 'arrow')
    .attr('viewBox', '0 -5 10 10')
    .attr('refX', 5)
    .attr('refY', 0)
    .attr('markerWidth', 6)
    .attr('markerHeight', 6)
    .attr('orient', 'auto')
    .append('path')
    .attr('d', 'M0,-5L10,0L0,5')
    .attr('fill', 'black')

  const treeX = 400
  const treeY = 200

  const tree = svg.append('g').attr('transform', `translate(${treeX}, ${treeY})`)

  const nodes = [
    { id: 0, x: 0, y: 0 },
    { id: 1, x: -100, y: 100 },
    { id: 2, x: 100, y: 100 },
    { id: 3, x: -120, y: 180 },
    { id: 4, x: -80, y: 180 },
    { id: 5, x: 80, y: 180 },
    { id: 6, x: 120, y: 180 }
  ]

  const links = [
    [0, 1], [0, 2],
    [1, 3], [1, 4],
    [2, 5], [2, 6]
  ]

  tree.selectAll('line')
    .data(links)
    .enter()
    .append('line')
    .attr('x1', d => nodes[d[0]].x)
    .attr('y1', d => nodes[d[0]].y)
    .attr('x2', d => nodes[d[1]].x)
    .attr('y2', d => nodes[d[1]].y)
    .attr('stroke', 'gray')
    .attr('class', d => `tree-link link-${d[1]}`)

  tree.selectAll('circle')
    .data(nodes)
    .enter()
    .append('circle')
    .attr('cx', d => d.x)
    .attr('cy', d => d.y)
    .attr('r', 8)
    .attr('fill', 'lightgray')

  // Animate sequence
  query.transition().delay(300).duration(500).attr('opacity', 1)

  C.forEach((c, i) => {
    c.transition().delay(1000 + i * 200).duration(300).attr('opacity', 1)
  })

  arrow.transition().delay(2000).duration(500)
    .attr('opacity', 1)
    .attr('x2', treeX - 20)

  d3.select('.link-3').transition().delay(2800).attr('stroke', 'green')
  d3.select('.link-6').transition().delay(3000).attr('stroke', 'green')
  d3.select('.link-5').transition().delay(3000).attr('stroke', 'gray')
})
</script>

<template>
  <div id="hash-tree-svg" class="w-full h-full flex justify-center items-center"></div>
</template>
