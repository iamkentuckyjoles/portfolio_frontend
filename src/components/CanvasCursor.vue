<template>
  <canvas id="canvas" ref="canvas" class="fixed top-0 left-0 w-screen h-screen pointer-events-none z-50"></canvas>
</template>

<script setup>
import { onMounted, onBeforeUnmount, ref } from 'vue'

const canvas = ref(null)
let ctx, f, pos = {}, lines = [], animationFrame

// Config
const E = {
  friction: 0.5,
  trails: 20,
  size: 50,
  dampening: 0.25,
  tension: 0.98,
}

function Node() {
  this.x = 0
  this.y = 0
  this.vy = 0
  this.vx = 0
}

function Oscillator(config) {
  this.phase = config.phase || 0
  this.offset = config.offset || 0
  this.frequency = config.frequency || 0.001
  this.amplitude = config.amplitude || 1
}
Oscillator.prototype.update = function () {
  this.phase += this.frequency
  return this.offset + Math.sin(this.phase) * this.amplitude
}

function Line(config) {
  this.spring = config.spring + 0.1 * Math.random() - 0.02
  this.friction = E.friction + 0.01 * Math.random() - 0.002
  this.nodes = []
  for (let i = 0; i < E.size; i++) {
    const node = new Node()
    node.x = pos.x
    node.y = pos.y
    this.nodes.push(node)
  }
}
Line.prototype.update = function () {
  let spring = this.spring
  let t = this.nodes[0]
  t.vx += (pos.x - t.x) * spring
  t.vy += (pos.y - t.y) * spring
  for (let i = 0; i < this.nodes.length; i++) {
    t = this.nodes[i]
    if (i > 0) {
      const prev = this.nodes[i - 1]
      t.vx += (prev.x - t.x) * spring
      t.vy += (prev.y - t.y) * spring
      t.vx += prev.vx * E.dampening
      t.vy += prev.vy * E.dampening
    }
    t.vx *= this.friction
    t.vy *= this.friction
    t.x += t.vx
    t.y += t.vy
    spring *= E.tension
  }
}
Line.prototype.draw = function () {
  ctx.beginPath()
  ctx.moveTo(this.nodes[0].x, this.nodes[0].y)
  for (let i = 1; i < this.nodes.length - 2; i++) {
    const n = this.nodes[i]
    const next = this.nodes[i + 1]
    const x = 0.5 * (n.x + next.x)
    const y = 0.5 * (n.y + next.y)
    ctx.quadraticCurveTo(n.x, n.y, x, y)
  }
  const last = this.nodes[this.nodes.length - 2]
  const end = this.nodes[this.nodes.length - 1]
  ctx.quadraticCurveTo(last.x, last.y, end.x, end.y)
  ctx.stroke()
  ctx.closePath()
}

function render() {
  ctx.globalCompositeOperation = 'source-over'
  ctx.clearRect(0, 0, ctx.canvas.width, ctx.canvas.height)
  ctx.globalCompositeOperation = 'lighter'
  ctx.strokeStyle = `hsla(${Math.round(f.update())},50%,50%,0.2)`
  ctx.lineWidth = 1
  for (let i = 0; i < E.trails; i++) {
    lines[i].update()
    lines[i].draw()
  }
  animationFrame = requestAnimationFrame(render)
}

function resizeCanvas() {
  ctx.canvas.width = window.innerWidth
  ctx.canvas.height = window.innerHeight
}

function onMouseMove(e) {
  pos.x = e.clientX
  pos.y = e.clientY
}

onMounted(() => {
  ctx = canvas.value.getContext('2d')
  f = new Oscillator({
    phase: Math.random() * 2 * Math.PI,
    amplitude: 85,
    frequency: 0.0015,
    offset: 285,
  })
  pos.x = window.innerWidth / 2
  pos.y = window.innerHeight / 2

  // create trails
  lines = []
  for (let i = 0; i < E.trails; i++) {
    lines.push(new Line({ spring: 0.4 + (i / E.trails) * 0.025 }))
  }

  resizeCanvas()
  window.addEventListener('resize', resizeCanvas)
  document.addEventListener('mousemove', onMouseMove)
  render()
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', resizeCanvas)
  document.removeEventListener('mousemove', onMouseMove)
  cancelAnimationFrame(animationFrame)
})
</script>
