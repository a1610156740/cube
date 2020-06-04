<template>
  <div class="body" @touchstart="touchStart" @touchmove="touchMove" @touchend="touchEnd">
    <div class="top-ui">
      <button>返回</button>
    </div>
    <div class="x" :style="{transform:'rotateX('+ calcY +'deg) rotateY('+ calcX +'deg)'}">
      <div class="y">
        <!--地板-->
        <div class="floor">
          <!--墙面 左-->
          <div class="left"></div>
          <!--墙面 右-->
          <div class="right"></div>
        </div>
        <!--天花板-->
        <div class="ceiling">
          <!--墙面 前-->
          <div class="front">
            <div class="menu">
              <div class="top">
                <button>菜单</button>
              </div>
            </div>
          </div>
          <!--墙面 后-->
          <div class="back"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      x: 0,
      y: 0,
      calcX: 0,
      calcY: 0,
      xToMove: 0,
      yToMove: 0
    };
  },
  created() {},
  mounted() {},
  methods: {
    touchStart(e) {
      let touch = e.touches[0];
      this.x = touch.clientX;
      this.y = touch.clientY;
    },
    touchMove(e) {
      let touch = e.touches[0];
      this.calcX = parseInt((this.x - touch.clientX) / 5) + this.xToMove;
      this.calcY = parseInt((touch.clientY - this.y) / 5) + this.yToMove;
      //console.log(this.calcX, this.calcY);
    },
    touchEnd(e) {
      //console.log(e);
      //let touch = e.changedTouches[0];
      this.x = 0;
      this.y = 0;
      this.xToMove = this.calcX;
      this.yToMove = this.calcY;
    }
  }
};
</script>

<style scoped type="text/css">
.top-ui {
  position: absolute;
  left: 0;
  top: 0;
  z-index: 10;
  padding: 20px;
}

div.menu {
  position: absolute;
  width: 140rem;
  height: 50%;
  left: 50%;
  margin-left: -70rem;
  top: 25%;
  background: rgba(0, 0, 0, 0.5);
  transform: rotateX(180deg);
  font-size: 10rem;
  display: flex;
}

div.menu button {
  font-size: 10rem;
}

.body {
  perspective: 50rem;
  overflow: hidden;
  width: 100%;
  height: 100%;
  margin: 0;
  display: flex;
  flex-wrap: wrap;
}

.body,
.ceiling,
.x,
.y,
.floor,
.right,
.left,
.front,
.back {
  transform-style: preserve-3d;
  box-sizing: border-box;
  position: absolute;
  content: "";
  left: 0;
  top: 0;
}
.x,
.y {
  position: absolute;
  top: -80rem;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  width: 1rem;
  height: 1rem;
}

.floor,
.floor .left,
.floor .right,
.ceiling,
.ceiling .front,
.ceiling .back {
  width: 300rem;
  height: 300rem;
  box-shadow: 0 0 1rem #0b0d0c;
}

.floor {
  background: url(../../assets/img/timg.jpg) no-repeat;
  background-size:100% 100%;
  transform: rotateX(90deg) translate3d(-150rem, 0, -50rem);
}

.floor .left,
.floor .right {
  background: url(../../assets/img/timg.jpg) no-repeat;
  background-size:100% 100%;
}

.floor .left {
  transform: rotateY(90deg) translate3d(-150rem, 0, -150rem);
}

.floor .right {
  transform: rotateY(-90deg) translate3d(150rem, 0, -150rem);
}

.ceiling {
  background: url(../../assets/img/timg.jpg) no-repeat;
  background-size:100% 100%;
  transform: rotateX(90deg) translate3d(-150rem, 0, 200rem);
}

.ceiling .front,
.ceiling .back {
  background: url(../../assets/img/timg.jpg) no-repeat;
  background-size:100% 100%;
}

.ceiling .front {
  transform: rotateX(90deg) translate3d(0, -150rem, 150rem);
}

.ceiling .back {
  transform: rotateX(90deg) translate3d(0, -150rem, -150rem);
}
</style>