<template>
  <div class="capsule-bar default-theme">
    <span class="capsule-bar-label" v-if="showLabel">{{label}}</span>
    <div class="capsule-bar-outer" @click="clickCapsule()">
      <div :class="{'capsule-bar-inner':true,'animate-move':isAnimated}" :style="InnerBarStyle"></div>
    </div>
    <span class="capsule-bar-text" v-if="showText">{{text}}</span>
  </div>
</template>

<script>
  export default {
    name: "Capsule",
    props: {
      showLabel: {
        default: true,
      },
      label: {
        type: String,
        default: 'label',
      },
      showText: {
        default: true,
      },
      text: {
        type: String,
        default: 'text',
      },
      innerheight: {
        default: "82%",
      },
      percentage: {
        type: Number,
        default: -1,
        validator: val => val >= 0 && val <= 100||-1
      },
      max: {
        type: Number,
        default: 100,
      },
      num: {
        type: Number,
        default: 80,
      },
      isAnimated:{
        default: true,
      }
    },
    computed: {
      InnerBarStyle() {
        const style = {};
        if (this.percentage === -1) {
          style.width = (this.num / this.max)*100 + '%'
        } else {
          style.width = this.percentage + '%';
        }
        style.height = this.innerheight;
        return style;
      }
    },
    created() {
    },
    methods: {
      clickCapsule() {
        this.$emit('clickCapsule')
      },
    }
  }
</script>

<style lang="less" scoped>
  .capsule-bar.default-theme {
    color: #ffffff;
  }

  .capsule-bar {
    position: relative;
    display: flex;
    justify-content: space-around;
    align-items: baseline;
    height: 15px;

    .capsule-bar-outer {
      background: rgba(119, 209, 255, 0);
      border: 1px solid #ffffff;
      border-radius: 10px;
      position: relative;
      height: 10px;
      width: 100px;
    }

    .capsule-bar-inner {
      background: #132eb8;
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      left: 1px;
      border-radius: 10px;
    }

    .capsule-bar-label {
      display: inline-block;
      width: 100px;
      text-align: center;
    }

    .capsule-bar-text {
      display: inline-block;
      width: 100px;
      text-align: center;
    }
  }

  .animate-move{

    animation: init-move 2s linear normal;
  }

  @keyframes init-move {
    0% {
      transform-origin:left top;
      transform: scaleX(0.1) translateY(-50%);

    }
    50% {
      transform-origin:left top;
      transform:  scaleX(0.75) translateY(-50%);
    }

    100% {
      transform-origin:left top;
      transform: scaleX(1) translateY(-50%);
    }
  }


</style>
