<template>
    <div class="flex flex-col items-center">
      <canvas ref="canvasRef" width="800" height="400" class="border rounded bg-gray-900"></canvas>
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
  
    // Hash indices on the right side
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
        color: '#ffffff',
        targetHash,
        stage: 0, // 0: moving to predictor, 1: routing to hash
      })
    }
  
    function draw() {
      ctx.clearRect(0, 0, width, height)
  
      // Draw predictor
      ctx.fillStyle = '#FFD93D'
      ctx.beginPath()
      ctx.rect(predictor.x - 40, predictor.y - 30, 80, 60)
      ctx.fill()
      ctx.strokeStyle = '#000'
      ctx.stroke()
      ctx.fillStyle = '#000'
      ctx.font = '14px sans-serif'
      ctx.textAlign = 'center'
      ctx.fillText('Predictor', predictor.x, predictor.y + 5)
  
      // Draw hashes
      hashes.forEach(h => {
        ctx.fillStyle = h.color
        ctx.beginPath()
        ctx.arc(h.x, h.y, 25, 0, Math.PI * 2)
        ctx.fill()
        ctx.fillStyle = '#fff'
        ctx.font = '12px sans-serif'
        ctx.textAlign = 'center'
        ctx.fillText(h.label, h.x, h.y + 40)
      })
  
      // Move and draw points
      points.forEach(p => {
        if (p.stage === 0) {
          // Move toward predictor
          const dx = predictor.x - p.x
          const dy = predictor.y - p.y
          const dist = Math.sqrt(dx * dx + dy * dy)
          if (dist > 2) {
            p.x += dx * 0.04
            p.y += dy * 0.04
          } else {
            p.stage = 1 // Reached predictor, now route to hash
          }
        } else if (p.stage === 1) {
          // Move toward selected hash
          const target = hashes[p.targetHash]
          const dx = target.x - p.x
          const dy = target.y - p.y
          const dist = Math.sqrt(dx * dx + dy * dy)
          if (dist > 2) {
            p.x += dx * 0.04
            p.y += dy * 0.04
          }
        }
  
        ctx.fillStyle = p.color
        ctx.beginPath()
        ctx.arc(p.x, p.y, 6, 0, Math.PI * 2)
        ctx.fill()
      })
  
      requestAnimationFrame(draw)
    }
  
    // Generate points every second
    setInterval(spawnPoint, 1200)
    draw()
  })
  </script>
  
  <style scoped>
  canvas {
    max-width: 100%;
  }
  </style>
  