<template>
    <div class="flex flex-col items-center">
      <canvas ref="canvasRef" width="600" height="350" class="border rounded bg-gray-900"></canvas>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue'
  
  const canvasRef = ref(null)
  
  onMounted(() => {
    const canvas = canvasRef.value
    const ctx = canvas.getContext('2d')
    const width = canvas.width
    const height = canvas.height
  
    const hashes = [
      { x: 100, y: 150, color: '#FF6B6B' },
      { x: 300, y: 150, color: '#4D96FF' },
      { x: 500, y: 150, color: '#1DD1A1' },
    ]
  
    let points = []
  
    function spawnPoint() {
      const point = {
        x: 50,
        y: Math.random() * (height - 40) + 20,
        targetHash: Math.floor(Math.random() * hashes.length),
      }
      points.push(point)
    }
  
    function draw() {
      ctx.clearRect(0, 0, width, height)
  
      // Draw hash nodes
      hashes.forEach(h => {
        ctx.fillStyle = h.color
        ctx.beginPath()
        ctx.arc(h.x, h.y, 20, 0, Math.PI * 2)
        ctx.fill()
  
        // Optional: label
        ctx.fillStyle = "#fff"
        ctx.font = "12px sans-serif"
        ctx.textAlign = "center"
        ctx.fillText("Hash", h.x, h.y + 35)
      })
  
      // Animate points
      points.forEach(p => {
        const target = hashes[p.targetHash]
        const dx = target.x - p.x
        const dy = target.y - p.y
        const dist = Math.sqrt(dx * dx + dy * dy)
  
        if (dist > 2) {
          p.x += dx * 0.05
          p.y += dy * 0.05
        }
  
        ctx.fillStyle = "#ffffff"
        ctx.beginPath()
        ctx.arc(p.x, p.y, 6, 0, Math.PI * 2)
        ctx.fill()
      })
  
      requestAnimationFrame(draw)
    }
  
    // Create points at intervals
    setInterval(spawnPoint, 1000)
    draw()
  })
  </script>
  
  <style scoped>
  canvas {
    max-width: 100%;
  }
  </style>
  