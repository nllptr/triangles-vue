<template>
  <div>
    <div class="type">{{ triangleType }}</div>
    <canvas ref="output" height="600" width="600" v-on:update="updateCanvas"></canvas>
  </div>
</template>

<script>
module.exports = {
  props: ["a", "b", "c"],
  data: function() {
    return {
      pointA: [0, 0],
      triangleType: 'Equilateral',
      scale: 100,
      valid: true
    }
  },
  computed: {
    ctx: function() {
      ctx = this.$refs.output.getContext('2d')
      ctx.lineWidth = 3
      return ctx
    },
    centerX: function() {
      const allX = [this.pointA[0], this.pointB[0], this.pointC[0]]
      const minX = Math.min(...allX)
      const maxX = Math.max(...allX)
      return (maxX + Math.abs(minX)) / 2
    },
    centerY: function() {
      const allY = [this.pointA[1], this.pointB[1], this.pointC[1]]
      const minY = Math.min(...allY)
      const maxY = Math.max(...allY)
      return (maxY + Math.abs(minY)) / 2
    },
    pointB: function() {
      return [this.pointA[0] + this.a * this.scale, this.pointA[1]]
    },
    pointC: function() {
      // Using method found on http://paulbourke.net/geometry/circlesphere/
      // Search in page for "Intersection of two circles"
      const dx = this.pointB[0] - this.pointA[0]
      const dy = this.pointB[1] - this.pointA[1]
      const d = this.a * this.scale
      const r0 = this.b * this.scale
      const r1 = this.c * this.scale

      this.valid = true
      if ((d >= r0 + r1) || (d < Math.abs(r0 - r1)) || (d == 0 && r0 == r2)) {
        this.valid = false
      }

      const a = (r0 * r0 - r1 * r1 + d * d) / (2 * d)
      const h = Math.sqrt(r0 * r0 - a * a)
      const x2 = this.pointA[0] + (a * dx / d)
      const y2 = this.pointA[1] + (a * dy / d)
      const x3 = x2 + (h * (this.pointB[1] - this.pointA[1]) / d)
      const y3 = y2 - (h * (this.pointB[0] - this.pointA[0]) / d)
      return [x3, y3]
    }
  },
  watch: {
    pointB: function() {
      this.drawCanvas()
    },
    pointC: function() {
      this.drawCanvas()
    }
  },
  methods: {
    drawCanvas: function() {
      this.ctx.clearRect(0, 0, 600, 600)
      this.ctx.translate(300 - this.centerX, 300 + this.centerY)
      this.ctx.beginPath()
      this.ctx.moveTo(...this.pointA)
      this.ctx.lineTo(...this.pointB)
      this.ctx.lineTo(...this.pointC)
      this.ctx.closePath()
      if (!this.valid) {
        this.triangleType = 'Not a valid triangle'
      } else if(this.a == this.b && this.b == this.c) {
        this.ctx.fillStyle = 'green'
        this.ctx.fill()
        this.ctx.strokeStyle = 'green'
        this.ctx.stroke()
        this.triangleType = 'Equilateral'
      } else if (this.a == this.b || this.a == this.c || this.b == this.c) {
        this.ctx.fillStyle = 'purple'
        this.ctx.fill()
        this.ctx.strokeStyle = 'purple'
        this.ctx.stroke()
        this.triangleType = 'Isosceles'
      } else {
        this.ctx.strokeStyle = '#2c3e50'
        this.ctx.stroke()
        this.triangleType = 'Scalene'
      }
      this.ctx.setTransform(1, 0, 0, 1, 0, 0);
    },
    updateCanvas: function() {
      this.drawCanvas()
    }
  },
  mounted: function() {
    this.updateCanvas()
  }
}
</script>

<style scoped>
.type {
  font-size: 3em;
}

canvas {
  height: 600px;
  width: 600px;
}
</style>