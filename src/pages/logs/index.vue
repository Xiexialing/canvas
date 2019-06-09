<template>
  <div>
    <canvas canvas-id="myCanvas" class="canvas" @touchstart="ontouchstart" @touchmove="ontouchmove"></canvas>
    <button @click="cleardraw" type="default">清除画板</button>
    <button @click="setSign" type="primary">提交签名</button>
    <img :src="imgSrc" alt="">
  </div>
</template>

<script>
  let ctx = '';
  export default {
    data() {
      return {
        pen: {
          color: '#00ff00',  // 画笔的颜色
          width: 5   // 画笔的粗细
        },
        imgSrc:''
      }
    },
    onReady() {
      this._initPen()
    },
    methods: {
      _initPen() {
        console.log(this)
        ctx = wx.createCanvasContext('myCanvas');
        ctx.setStrokeStyle(this.pen.color);
        ctx.setLineWidth(this.pen.width);
        ctx.setLineCap('round');
        ctx.setLineJoin('round');
      },
      ontouchstart(e) {
        let {x, y} = e.touches[0];
        ctx.moveTo(x, y)
      },
      ontouchmove(e) {
        let {x, y} = e.touches[0];
        ctx.lineTo(x, y);
        ctx.stroke();
        ctx.draw(true);
        ctx.moveTo(x, y)
      },

      cleardraw() {
        ctx.clearRect(0, 0, 375, 300);
        ctx.draw(true);
      },
      // 提交签名内容
      setSign() {
        let that = this;
        wx.canvasToTempFilePath({
          canvasId: 'myCanvas',
          success(res) {
            that.imgSrc = res.tempFilePath
          }
        })
      }
    }
  }
</script>

<style>
  .canvas {
    width: 100%;
    height: 600rpx;
    background-color: #e9e9e9;
  }
</style>
