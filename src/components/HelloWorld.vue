<template>
  <div
    @touchstart="start($event)"
    @touchmove="move($event)"
    @touchend="end($event)"
  >
    <div class="box" :class="setclass()">1</div>
    <div class="box2" :class="setclass2()">2</div>
    <div class="box3" :class="setclass3()">3</div>
    <!-- <div :class="setclass(i)"  v-for="(v, i) in 3" :key="i">{{ v }}</div> -->
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      leftshow: false,
      rightshow: false,
      num: 0,
      rightnum: 0,
    };
  },
  methods: {
    setclass() {
      console.log(this.num, this.rightnum);
      let name = "";
      if (this.num == 1) {
        if (this.leftshow) {
          name = "leftmove";
        }
      }

      if (this.num == 2) {
        if (this.leftshow) {
          name = "leftmove3";
        }
      }
      if (this.num == 3) {
        if (this.leftshow) {
          name = "leftmove2";
        }
      }
      if (this.rightnum == 1) {
        if (this.rightshow) {
          name = "rightmove";
        }
      }
      if (this.rightnum == 2) {
        if (this.rightshow) {
          name = "rightmove2";
        }
      }
      if (this.rightnum == 3) {
        if (this.rightshow) {
          name = "rightmove3";
        }
      }
      // if (this.rightshow) {
      //   name = "rightmove";
      // }
      return name;
    },
    setclass2() {
      let name = "";

      if (this.num == 1) {
        if (this.leftshow) {
          name = "leftmove2";
        }
      }
      if (this.num == 2) {
        if (this.leftshow) {
          name = "leftmove";
        }
      }
      if (this.num == 3) {
        if (this.leftshow) {
          name = "leftmove3";
        }
      }
      if (this.rightnum == 1) {
        if (this.rightshow) {
          name = "rightmove2";
        }
      }
      if (this.rightnum == 2) {
        if (this.rightshow) {
          name = "rightmove3";
        }
      }
      if (this.rightnum == 3) {
        if (this.rightshow) {
          name = "rightmove";
        }
      }
      // if (this.rightshow) {
      //   name = "rightmove2";
      // }
      return name;
    },
    setclass3() {
      let name = "";

      if (this.num == 1) {
        if (this.leftshow) {
          name = "leftmove3";
        }
      }
      if (this.num == 2) {
        if (this.leftshow) {
          name = "leftmove2";
        }
      }
      if (this.num == 3) {
        if (this.leftshow) {
          name = "leftmove";
        }
      }
      if (this.rightnum == 1) {
        if (this.rightshow) {
          name = "rightmove3";
        }
      }
      if (this.rightnum == 2) {
        if (this.rightshow) {
          name = "rightmove";
        }
      }
      if (this.rightnum == 3) {
        if (this.rightshow) {
          name = "rightmove2";
        }
      }
      // if (this.rightshow) {
      //   name = "rightmove3";
      // }
      return name;
    },
    // 左右滑动事件
    getAngle(angx, angy) {
      return (Math.atan2(angy, angx) * 180) / Math.PI;
    },
    getDirection(startx, starty, endx, endy) {
      var angx = endx - startx;
      var angy = endy - starty;
      var result = 0; //默认标记没有滑动
      //如果滑动距离太短
      if (Math.abs(angx) < 2 && Math.abs(angy) < 2) {
        return result;
      }
      var angle = this.getAngle(angx, angy);
      if (angle >= -135 && angle <= -45) {
        result = 1; //向上
      } else if (angle > 45 && angle < 135) {
        result = 2; //向下
      } else if (
        (angle >= 135 && angle <= 180) ||
        (angle >= -180 && angle < -135)
      ) {
        result = 3; //向左
      } else if (angle >= -45 && angle <= 45) {
        result = 4; //向右
      }
      return result;
    },
    start(event) {
      let tabbarRef = this.$refs.tabbarRef;
      let touchS = event.targetTouches[0]; //touches数组对象获得屏幕上所有的touch，取第一个touch
      this.startPos = {
        x: touchS.pageX,
        y: touchS.pageY,
        time: new Date(),
      }; //取第一个touch的坐标值
    },
    move(event) {
      //当屏幕有多个touch或者页面被缩放过，就不执行move操作
      if (event.targetTouches.length > 1 || (event.scale && event.scale !== 1))
        return;
    },
    end(event) {
      let touchE = event.changedTouches[0];
      this.endPos = {
        x: touchE.pageX,
        y: touchE.pageY,
        timeStemp: new Date(),
      };
      let direction = this.getDirection(
        this.startPos.x,
        this.startPos.y,
        this.endPos.x,
        this.endPos.y
      );
      // console.log(direction);
      if (direction == 3) {
        if (this.leftshow) {
          this.rightnum = this.num + 1;
          this.num = 0;
        }
        if (this.rightnum >= 3) {
          this.rightnum = 0;
        }

        this.rightnum += 1;
        this.leftshow = false;
        this.rightshow = true;
      }
      if (direction == 4) {
        if (this.rightshow) {
          this.num = this.rightnum + 1;
          this.rightnum = 0;
        }
        if (this.num >= 3) {
          this.num = 0;
        }

        this.num += 1;
        this.rightshow = false;
        this.leftshow = true;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style  scoped>
.box {
  width: 80px;
  height: 80px;
  background: #ccc;
  border-radius: 50%;
  position: fixed;
  left: 400px;
  top: 400px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.leftmove {
  animation: leftmove 2s forwards;
}
.rightmove {
  animation: rightmove 2s forwards;
}

.box2 {
  width: 80px;
  height: 80px;
  background: #ccc;
  border-radius: 50%;
  position: fixed;
  left: 300px;
  top: 370px;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0.5;
}
.leftmove2 {
  animation: leftmove2 2s forwards;
}
.rightmove2 {
  animation: rightmove2 2s forwards;
}

.box3 {
  width: 80px;
  height: 80px;
  background: #ccc;
  border-radius: 50%;
  position: fixed;
  left: 500px;
  top: 370px;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0.5;
}
.leftmove3 {
  animation: leftmove3 2s forwards;
}
.rightmove3 {
  animation: rightmove3 2s forwards;
}

@keyframes leftmove {
  from {
    top: 400px;
    left: 400px;
  }

  to {
    left: 500px;
    top: 370px;
  }
}

@keyframes leftmove2 {
  from {
    left: 300px;
    top: 370px;
  }

  to {
    left: 400px;
    top: 400px;
  }
}

@keyframes leftmove3 {
  from {
    left: 500px;
    top: 370px;
  }

  to {
    left: 300px;
    top: 370px;
  }
}

@keyframes rightmove {
  from {
    top: 400px;
    left: 400px;
  }

  to {
    left: 300px;
    top: 370px;
  }
}

@keyframes rightmove2 {
  from {
    left: 300px;
    top: 370px;
  }

  to {
    left: 500px;
    top: 370px;
  }
}

@keyframes rightmove3 {
  from {
    left: 500px;
    top: 370px;
  }

  to {
    top: 400px;
    left: 400px;
  }
}
</style>
