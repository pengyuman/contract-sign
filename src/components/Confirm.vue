<template>
  <div class="confirm"
       v-show="isShowConfirm">
    <!-- <div class="confirm" v-show="show"> -->
    <div class="mask"></div>
    <div class="content"
         :style="contentStyle">
      <div class="icon-top"
           :class="logoClass"></div>
      <div class="main"
           :class="mainClass">
        <div class="title"
             v-html="titleText"></div>
        <div class="text"
             v-html="content"></div>
      </div>
      <div class="btns">
        <button type="button"
                class="btn btn-cancel"
                @click="clickFun('clickCancel')"
                v-if="type === 'confirm'">{{cancelText}}</button>
        <button type="button"
                class="btn btn-continue"
                @click="clickFun('clickConfirm')">{{confirmText}}</button>
      </div>
    </div>
  </div>
</template>
<script>
// 使用方式：
// 打开：this.$refs.myConfirm.show(configObj)
// 关闭：this.$refs.myConfirm.hidden()
export default {
  name: 'Confirm',
  data () {
    return {
      isShowConfirm: false, // 用于控制整个窗口的显示/隐藏
      titleText: '操作提示', // 提示框标题
      content: '', // 提示框的内容
      cancelText: '取消', // 取消按钮的文字
      confirmText: '确认', // 确认按钮的文字
      logoClass: 'icon-statement',
      contentStyle: '',
      mainClass: '',
      type: 'alert', // 表明弹框的类型：confirm - 确认弹窗（有取消按钮）；alert - 通知弹框（没有取消按钮）
      outerData: null // 用于记录外部传进来的数据，也可以给外部监听userBehavior，事件的函数提供判断到底是哪个事件触发的
    }
  },
  // props: {
  //   show: {
  //     type: Boolean,
  //     default: false
  //   }
  // },
  // model: {
  //   prop: 'show',
  //   event: 'change'
  // },
  methods: {
    // handleCancel () {
    //   this.$emit('change', false)
    // },
    show (config) {
      if (Object.prototype.toString.call(config) === '[object Object]') {
        // 确保传递的是一个对象
        this.titleText = config.titleText || '操作提示'
        this.content = config.content || ''
        this.logoClass = config.logoClass || 'icon-statement'
        this.contentStyle = config.contentStyle || ''
        this.mainClass = config.mainClass || ''
        this.cancelText = config.cancelText || '取消'
        this.confirmText = config.confirmText || '确认'
        this.type = config.type || 'alert'
        this.outerData = config.data || null
      }
      this.isShowConfirm = true
    },
    hidden () {
      this.isShowConfirm = false
      this.titleText = '操作提示'
      this.cancelText = '取消'
      this.confirmText = '确认'
      this.type = 'alert'
      this.outerData = null
      this.logoClass = ''
      this.contentStyle = ''
      this.mainClass = ''
    },
    clickFun (type) {
      this.$emit('userBehavior', type, this.outerData)
      this.hidden()
    }
  }
}
</script>
<style lang="less" scoped>
.confirm {
  position: fixed;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
  z-index: 9;
  .mask {
    position: absolute;
    width: 100%;
    height: 100%;
    opacity: 0.6;
    background-color: #000;
  }
}
.content {
  width: 4.8rem;
  box-sizing: border-box;
  border-radius: 0.15rem;
  background-color: #fff;
  font-size: 0.3rem;
  position: relative;
  overflow: hidden;
  color: #b3b3b3;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  // display: flex;
  // flex-direction: column;
  .icon-top {
    width: 1rem;
    height: 1rem;
    margin: 0.55rem auto 0;
  }
  .icon-statement {
    background: url(../assets/images/logo-statement-alert.png) no-repeat;
    background-size: 100% auto;
  }
  .none {
    background: none;
    height: 0.2rem;
  }
  .icon-pay {
    background: url(../assets/images/logo-pay-alert.png) no-repeat;
    background-size: 100% auto;
  }
  .icon-email {
    background: url(../assets/images/logo-email-alert.png) no-repeat;
    background-size: 100% auto;
  }
  .icon-upload {
    background: url(../assets/images/logo-pay-success-alert.png) no-repeat;
    background-size: 100% auto;
  }
  .main {
    padding: 0.2rem 0.4rem 0.6rem 0.4rem;
    .title {
      font-size: 0.36rem;
      text-align: center;
      // font-style: italic;
      font-stretch: normal;
      line-height: 0.48rem;
      letter-spacing: 0.01rem;
      color: #3b8492;
      margin-bottom: 0.36rem;
    }
  }
  .change-text {
    .text {
      text-align: center;
    }
  }
  .over-scroll {
    max-height: 60vh;
    overflow-y: scroll;
  }
  .btns {
    // margin-top: 0.76rem;
    display: flex;
  }
  .btn {
    width: 100%;
    height: 0.8rem;
    background-color: #552f5b;
    line-height: 0.8rem;
    text-align: center;
    color: #fff;
    border: none;
  }
  .btn-cancel {
    background-color: #aba2b3;
  }
}
</style>
