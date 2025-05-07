<template>
    <div class="w-full flex justify-center">
      <canvas ref="canvasRef" width="800" height="400" class="rounded"></canvas>
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
      { x: 700, y: 100, color: '#FF6B6B', label: 'Hash A' },
      { x: 700, y: 200, color: '#4D96FF', label: 'Hash B' },
      { x: 700, y: 300, color: '#1DD1A1', label: 'Hash C' },
    ]
  
    const predictor = { x: 400, y: 200 }
  
    let points = []
  
    function spawnPoint() {
      const y = Math.random() * 300 + 50
      const targetHash = Math.floor(Math.random() * hashes.length)
      points.push({
        x: 50,
        y,
        color: '#555',
        targetHash,
        stage: 0,
      })
    }
  
    function draw() {
      ctx.clearRect(0, 0, width, height)
  
      // Draw predictor
      ctx.fillStyle = '#FFD93D'
      ctx.beginPath()
      ctx.roundRect(predictor.x - 40, predictor.y - 30, 80, 60, 10)
      ctx.fill()
      ctx.fillStyle = '#000'
      ctx.font = '14px sans-serif'
      ctx.textAlign = 'center'
      ctx.fillText('Predictor', predictor.x, predictor.y + 5)
  
      // Draw hashes
      hashes.forEach(h => {
        ctx.fillStyle = h.color
        ctx.beginPath()
        ctx.arc(h.x, h.y, 22, 0, Math.PI * 2)
        ctx.fill()
  
        ctx.fillStyle = '#333'
        ctx.font = '13px sans-serif'
        ctx.textAlign = 'center'
        ctx.fillText(h.label, h.x, h.y + 38)
      })
  
      // Move and draw points
      points.forEach(p => {
        const target = p.stage === 0 ? predictor : hashes[p.targetHash]
        const dx = target.x - p.x
        const dy = target.y - p.y
        const dist = Math.sqrt(dx * dx + dy * dy)
  
        if (dist > 2) {
          p.x += dx * 0.04
          p.y += dy * 0.04
        } else if (p.stage === 0) {
          p.stage = 1
        }
  
        ctx.fillStyle = p.color
        ctx.beginPath()
        ctx.arc(p.x, p.y, 5.5, 0, Math.PI * 2)
        ctx.fill()
      })
  
      requestAnimationFrame(draw)
    }
  
    setInterval(spawnPoint, 1200)
    draw()
  })
  </script>
  
  <style scoped>
  canvas {
    background-color: transparent;
  }
  </style>
  