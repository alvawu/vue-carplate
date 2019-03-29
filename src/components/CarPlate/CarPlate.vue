<template>
<div>
  <div @click.stop="show" :class="valueClass">{{displayValue}}</div>
  <transition name="custom-classes-transition" enter-active-class="animated fadeIn" leave-active-class="animated fadeOut">
    <div class="carno" v-if="shown" @click="cancel">
      <ul>
        <li class="carno_digit" v-for="(digit, i) in carnoArr" :class="{'current': current === i}" @click.stop="onClickDigit(i)"
          v-html="digit"></li>
      </ul>
      <div class="err" v-if="errMsg">{{errMsg}}</div>
    </div>
  </transition>
  <transition name="custom-classes-transition" enter-active-class="animated slideInUp" leave-active-class="animated slideOutDown">
    <div class="keyboard" v-if="shown">
      <div style="position: relative">
        <div class="header">
          <span class="clearNo" @click="clear">清除</span>
          <span class="confirm" @click="confirm">完成</span>
        </div>
        <div class="line" v-if="current === 0" :class="line.size" v-for="line in carTxt">
          <div class="key" :class="{'delete': key === 'delete'}" v-for="key in line.name" @click="onClickKey(key, line.type)">
            <i class="iconfont icon-tuige" v-if="key === 'delete'"></i>
            <span v-else>{{key}}</span>
          </div>
        </div>

        <div class="line" v-if="current > 0" :class="line.size" v-for="line in numAlphaText">
          <div class="key" :class="{'delete': key === 'delete', 'disabled': current === 1 && line.type === 'number'}"
            v-for="key in line.name" @click="onClickKey(key, line.type)">
            <i class="iconfont icon-tuige" v-if="key === 'delete'"></i>
            <span v-else>{{key}}</span>
          </div>
        </div>
      </div>
    </div>
  </transition>

</div>
</template>

<style src="../../assets/iconfont/iconfont.css" lang="css"></style>
<style scoped>
@keyframes cursor {
    0% {
        border-color: #4983ff;
        color: #4983ff;
    }
    50% {
        border-color: #ffffff;
        color: #ffffff;
    }
    100% {
        border-color: #4983ff;
        color: #4983ff;
    }
}

ul {
    margin: 0;
    padding: 0;
}

.header {
    height: 30px;
    line-height: 30px;
    background: #ffffff;
    border-bottom: 1px solid #efefef;
    padding: 0 10px;
    margin-bottom: 10px;
    font-size: 14px;
}

.header .clearNo {
    float: left;
    color: #666666;
}

.header .confirm {
    float: right;
    color: #4983ff;
}
.carno {
    position: fixed;
    top: 0px;
    left: 0px;
    width: 100%;
    height: 100.1%;
    padding-top: 30%;
    /* margin-left: -0.5rem; */
    text-align: center;
    background-color: rgba(0, 0, 0, 0.8);
    vertical-align: baseline;
}
.carno .carno_digit{
    display: inline-block;
    width: 8%;
    height: 40px;
    line-height: 40px;
    margin-right: 2vw;
    color: #ffffff;
    font-size: 24px;
    border-bottom: 2px solid #ffffff;
}
.carno .carno_digit:nth-child(2) {
    margin-right: 20px;
}
.carno .carno_digit.current{
    color: #4983ff;
    border-color: #4983ff;
    animation: cursor 1s infinite ease-in-out;
    -webkit-animation: cursor 1s infinite ease-in-out;
}
.errMsg {
    color: #ffffff;
}
.keyboard{
    position: fixed;
    bottom: 0px;
    left: 0px;
    width: 100%;
    height: auto;
    background: rgb(238, 238, 238);
    z-index: 1000;
    padding-bottom: 10px;
}
.line{
    text-align: center;
}
.key{
    display: inline-block;
    background: #ffffff;
    border-radius: 5px;
    margin: 0.8vw;
    padding: 0;
    height: 20px;
    line-height: 20px;
    text-align: center;
    box-shadow: 0px 0px 2px #7B98B1;
    width: 20px;
    font-size: 14px;
}
.key i {
    font-size: 14px;
}
.key:active{
    background: #7B98B1;
    color: #ffffff;
}

.key.disabled{
    background: #dddddd;
}

.key.delete{
    background: #7B98B1;
    color: #ffffff;
}

.key.delete:active{
    color: #7B98B1;
    background: #ffffff;
}

.line.big .key{
    height: 10vw;
    line-height: 10vw;
    width: 10vw;
}

.line.normal .key{
    height: 8vw;
    line-height: 8vw;
    width: 8vw;
}

.line.normal .key i{
    font-size: 12px;
}

.line.mini .key{
    height: 6vw;
    width: 6vw;
}

.err{
    margin-top: 15vh;
    color: #fff;
}

.animated {
  -webkit-animation-duration: 0.5s;
  animation-duration: 0.5s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}

@media (prefers-reduced-motion) {
  .animated {
    -webkit-animation: unset !important;
    animation: unset !important;
    -webkit-transition: none !important;
    transition: none !important;
  }
}

@-webkit-keyframes fadeIn {
  from {
    opacity: 0;
  }

  to {
    opacity: 1;
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }

  to {
    opacity: 1;
  }
}

.fadeIn {
  -webkit-animation-name: fadeIn;
  animation-name: fadeIn;
}

@-webkit-keyframes fadeOut {
  from {
    opacity: 1;
  }

  to {
    opacity: 0;
  }
}

@keyframes fadeOut {
  from {
    opacity: 1;
  }

  to {
    opacity: 0;
  }
}

.fadeOut {
  -webkit-animation-name: fadeOut;
  animation-name: fadeOut;
}


@-webkit-keyframes slideInUp {
  from {
    -webkit-transform: translate3d(0, 100%, 0);
    transform: translate3d(0, 100%, 0);
    visibility: visible;
  }

  to {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

@keyframes slideInUp {
  from {
    -webkit-transform: translate3d(0, 100%, 0);
    transform: translate3d(0, 100%, 0);
    visibility: visible;
  }

  to {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

.slideInUp {
  -webkit-animation-name: slideInUp;
  animation-name: slideInUp;
}

@-webkit-keyframes slideOutDown {
  from {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }

  to {
    visibility: hidden;
    -webkit-transform: translate3d(0, 100%, 0);
    transform: translate3d(0, 100%, 0);
  }
}

@keyframes slideOutDown {
  from {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }

  to {
    visibility: hidden;
    -webkit-transform: translate3d(0, 100%, 0);
    transform: translate3d(0, 100%, 0);
  }
}

.slideOutDown {
  -webkit-animation-name: slideOutDown;
  animation-name: slideOutDown;
}

.empty {
    color: rgb(169, 169, 169)
}
</style>
<script>
import Vue from 'vue'
// import { TransferDom } from 'vux'
export default {
    name: 'car-plate',
    // directives: {TransferDom},
    components: {},
    data: function () {
        return {
            shown: false,
            current: 0,
            valueClass: 'empty',
            carnoArr: ['&nbsp;', '&nbsp;', '&nbsp;', '&nbsp;', '&nbsp;', '&nbsp;', '&nbsp;', '&nbsp;'],
            errMsg: '',
            carTxt: [{
                name: ['粤', '京', '冀', '沪', '津', '晋', '蒙', '辽'],
                size: 'big',
                type: 'province'
            }, {
                name: ['苏', '浙', '皖', '闽', '赣', '鲁', '豫', '鄂'],
                size: 'big',
                type: 'province'
            }, {
                name: ['琼', '渝', '川', '贵', '云', '藏', '陕', '甘'],
                size: 'big',
                type: 'province'
            }, {
                name: ['吉', '黑', '湘', '桂', '青', '宁', '新', 'delete'],
                size: 'big',
                type: 'province'
            }],
            numAlphaText: [{
                name: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0'],
                size: 'normal',
                type: 'number'
            }, {
                name: ['Q', 'W', 'E', 'R', 'T', 'Y', 'U', 'I', 'O', 'P'],
                size: 'normal',
                type: 'alpha'
            }, {
                name: ['A', 'S', 'D', 'F', 'G', 'H', 'J', 'K', 'L'],
                size: 'normal',
                type: 'alpha'
            }, {
                name: ['Z', 'X', 'C', 'V', 'B', 'N', 'M', 'delete'],
                size: 'normal',
                type: 'alpha'
            }]
        }
    },
    props: {
        value: [String]
    },
    mounted: function () {
    },
    watch: {
        currentValue: function (val) {
        },
        value: function (val) {
        }
    },
    computed: {
        displayValue: function () {
            let self = this
            let disp = []
            let valueArr = self.value.split('')
            valueArr.forEach(function (f, i) {
                disp.push(f)
                if (i === 1) {
                    disp.push(' ')
                }
            })
            if (disp.length >= 7) {
                self.valueClass = ''
                return disp.join('')
            } else {
                self.valueClass = 'empty'
                return '请点击录入车牌号'
            }
        }
    },
    methods: {
        show: function () {
            let self = this
            document.activeElement.blur()
            let valueArr = self.value.split('')
            for (let i = 0; i <= 7; i++) {
                if (valueArr[i]) {
                    Vue.set(self.carnoArr, i, valueArr[i])
                } else {
                    Vue.set(self.carnoArr, i, '&nbsp;')
                }
            }
            var scrollTop = document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop
            window.scrollTo(0, scrollTop + 1)
            self.current = 0
            self.shown = true
        },

        onClickDigit: function (c) {
            this.current = c
        },

        onClickKey: function (key, type) {
            let self = this
            self.errMsg = ''
            if (key === 'delete') {
                Vue.set(this.carnoArr, self.current, '&nbsp;')
                if (self.current > 0) {
                    self.current--
                }
            } else if (self.current === 1 && type === 'number') {
            } else {
                Vue.set(this.carnoArr, self.current, key)
                if (self.current < self.carnoArr.length - 1) {
                    self.current++
                }
            }
        },

        confirm: function () {
            let self = this
            let newValue = []
            self.carnoArr.forEach(function (digit, index) {
                if (digit !== '&nbsp;') {
                    newValue.push(digit)
                }
            })
            console.log(newValue)
            if (newValue.length > 0 && newValue.length < 7) {
                self.errMsg = '请填写完整车牌号'
            } else {
                self.$emit('input', newValue.join(''))
                self.shown = false
            }
        },

        clear: function () {
            this.carnoArr = ['&nbsp;', '&nbsp;', '&nbsp;', '&nbsp;', '&nbsp;', '&nbsp;', '&nbsp;', '&nbsp;']
            this.current = 0
            // this.shown = false
        },

        cancel: function () {
            this.shown = false
        }
    }
}
</script>