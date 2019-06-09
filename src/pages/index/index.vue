<template>
  <div>
    <div class="canvas-area">
      <canvas canvas-id="myCanvas" class="mycanvas"></canvas>
    </div>
    <form>
      <div class="form-item">
        <label class="form-label">网址：</label>
        <input type="text" class="form-control" :placeholder="placeholder" v-model="url">
      </div>
      <div>
        <button type="primary" class="confirm-btn" @click="confirm">确  定</button>
      </div>
    </form>
  </div>
</template>

<script>
  import drawQrcode from 'weapp-qrcode'

  export default {
    data() {
      return {
        width: 200,
        height: 200,
        url: '',
        placeholder: 'http://www.baidu.com'
      }
    },

    methods: {
      draw() {
        this.showLoading()
        drawQrcode({
          width: this.width,
          height: this.height,
          canvasId: 'myCanvas',
          text: this.url || this.placeholder
        })
      },
      confirm() {
        this.draw()
      },
      showLoading() {
        wx.showToast({
          title: '加载中...',
          icon: 'loading',
          duration: 1000
        })
      }
    },

    mounted() {
      this.draw()
    }
  }
</script>

<style scoped>
  .canvas-area{
    margin-top: 64rpx;
    padding: 12rpx;
    text-align: center;
  }
  .mycanvas{
    width: 200px;
    height: 200px;
    margin: 0 auto;
  }
  .form-label{
    margin: 12rpx 24rpx;
    font-size: 32rpx;
    color: #999;
  }
  .form-control{
    margin: 12rpx 24rpx;
    height: 92rpx;
    line-height: 92rpx;
    padding: 0 12rpx;
    border-radius: 12rpx;
    border: 1px solid #e9e9e9;
  }
  .confirm-btn{
    margin: 12rpx 24rpx;
  }
</style>
