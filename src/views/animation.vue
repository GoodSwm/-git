<template>
  <div
    @touchstart="start($event)"
    @touchmove="move($event)"
    @touchend="end($event)"
  >
    <div class="box" v-for="(v, i) in 7" :key="i">{{ i }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      num: 0,
      numm: 0,
      leftshow: false,
      rightshow: false,
    };
  },
  methods: {
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
        console.log("左滑");
        let list = ["a", "b", "c", "d", "e", "f", "g"];
        let list2 = ["aa", "bb", "cc", "dd", "ee", "ff", "gg"];
        let list3 = ["aaa", "bbb", "ccc", "ddd", "eee", "fff", "ggg"];
        let list4 = ["aaaa", "bbbb", "cccc", "dddd", "eeee", "ffff", "gggg"];
        let list5 = [
          "aaaaa",
          "bbbbb",
          "ccccc",
          "ddddd",
          "eeeee",
          "fffff",
          "ggggg",
        ];
        let list6 = [
          "aaaaaa",
          "bbbbbb",
          "cccccc",
          "dddddd",
          "eeeeee",
          "ffffff",
          "gggggg",
        ];
        let list7 = [
          "aaaaaaa",
          "bbbbbbb",
          "ccccccc",
          "ddddddd",
          "eeeeeee",
          "fffffff",
          "ggggggg",
        ];
        // this.num = this.numm + 5;
        // this.numm = 0;
        if (this.rightshow) {
          this.num = 7 - this.numm
          this.numm = 0;
        }
        this.num += 1;
        if (this.num == 1) {
          this.leftmeth(list);
        }
        if (this.num == 2) {
          this.leftmeth(list2);
        }
        if (this.num == 3) {
          this.leftmeth(list3);
        }
        if (this.num == 4) {
          this.leftmeth(list4);
        }
        if (this.num == 5) {
          this.leftmeth(list5);
        }
        if (this.num == 6) {
          this.leftmeth(list6);
        }
        if (this.num == 7) {
          this.leftmeth(list7);
        }

        if (this.num >= 7) {
          this.num = 0;
        }
        this.leftshow = true;
        this.rightshow = false;
      }
      if (direction == 4) {
        console.log("右滑");
        let list = ["as", "bs", "cs", "ds", "es", "fs", "gs"];
        let list2 = ["aas", "bbs", "ccs", "dds", "ees", "ffs", "ggs"];
        let list3 = ["aaas", "bbbs", "cccs", "ddds", "eees", "fffs", "gggs"];
        let list4 = ["aaaas", "bbbbs", "ccccs", "dddds", "eeees", "ffffs", "ggggs"];
        let list5 = [
          "aaaaas",
          "bbbbbs",
          "cccccs",
          "ddddds",
          "eeeees",
          "fffffs",
          "gggggs",
        ];
        let list6 = [
          "aaaaaas",
          "bbbbbbs",
          "ccccccs",
          "dddddds",
          "eeeeees",
          "ffffffs",
          "ggggggs",
        ];
        let list7 = [
          "aaaaaaas",
          "bbbbbbbs",
          "cccccccs",
          "ddddddds",
          "eeeeeees",
          "fffffffs",
          "gggggggs",
        ];
        if (this.leftshow) {
          this.numm = 7 - this.num ;
          this.num = 0;
        }
        this.numm += 1;
        if (this.numm == 1) {
          this.rightmeth(list);
        }
        if (this.numm == 2) {
          this.rightmeth(list2);
        }
        if (this.numm == 3) {
          this.rightmeth(list3);
        }
        if (this.numm == 4) {
          this.rightmeth(list4);
        }
        if (this.numm == 5) {
          this.rightmeth(list5);
        }
        if (this.numm == 6) {
          this.rightmeth(list6);
        }
        if (this.numm == 7) {
          this.rightmeth(list7);
        }
        if (this.numm >= 7) {
          this.numm = 0;
        }
        this.leftshow = false;
        this.rightshow = true;
      }
    },
    rightmeth(list) {
      let dom = document.getElementsByClassName("box");
      console.log(dom.length);
      list.forEach((v, i) => {
        let styleSheetslist = document.styleSheets[0];
        styleSheetslist.insertRule(
          `@keyframes ${v}example {
                    from {
                        top: ${this.setoff(dom[i].offsetTop, i)}px;
                        left: ${this.setoff(dom[i].offsetLeft, i)}px;
                        }
                        to {
                        top: ${this.setrtop(dom[i].offsetTop, i)}px;
                        left: ${this.setrleft(dom[i].offsetLeft, i)}px;
                        }
                    }`,
          0
        );
        dom[i].style.animation = `${v}example 1s forwards`;
      });
    },
    leftmeth(list) {
      let dom = document.getElementsByClassName("box");
      console.log(dom.length);
      list.forEach((v, i) => {
        let styleSheetslist = document.styleSheets[0];
        styleSheetslist.insertRule(
          `@keyframes ${v}example {
                    from {
                        top: ${this.setoff(dom[i].offsetTop, i)}px;
                        left: ${this.setoff(dom[i].offsetLeft, i)}px;
                        }
                        to {
                        top: ${this.setofftop(dom[i].offsetTop, i)}px;
                        left: ${this.setoffleft(dom[i].offsetLeft, i)}px;
                        }
                    }`,
          0
        );
        dom[i].style.animation = `${v}example 1s forwards`;
      });
    },
    setoff(v, i) {
      return v;
    },
    setrleft(v, i) {
      let value = "";
      if (this.numm == 1) {
        if (i <= 2 && i > 0) {
          value = v - 100;
        }
        if (i == 3) {
          value = v - 100;
        }
        if (i > 3 && i <= 6) {
          value = v - 100;
        }
        if (i == 0) {
          value = v + 600;
        }
      }
      if (this.numm == 2) {
        if (i <= 4 && i > 1) {
          value = v - 100;
        }
        if (i > 4 || i == 0) {
          value = v - 100;
        }
        if (i == 1) {
          value = v + 600;
        }
      }
      if (this.numm == 3) {
        if (i <= 5 && i > 2) {
          value = v - 100;
        }
        if (i <= 1 || i == 6) {
          value = v - 100;
        }
        if (i == 2) {
          value = v + 600;
        }
      }
      if (this.numm == 4) {
        if (i <= 6 && i > 3) {
          value = v - 100;
        }
        if (i <= 2) {
          value = v - 100;
        }
        if (i == 3) {
          value = v + 600;
        }
      }
      if (this.numm == 5) {
        if (i == 0 || i >= 5) {
          value = v - 100;
        }
        if (i <= 3 && i > 0) {
          value = v - 100;
        }
        if (i == 4) {
          value = v + 600;
        }
      }
      if (this.numm == 6) {
        if (i == 6 || i <= 1) {
          value = v - 100;
        }
        if (i <= 4 && i > 1) {
          value = v - 100;
        }
        if (i == 5) {
          value = v + 600;
        }
      }
      if (this.numm == 7) {
        if (i <= 2) {
          value = v - 100;
        }
        if (i <= 5 && i > 2) {
          value = v - 100;
        }
        if (i == 6) {
          value = v + 600;
        }
      }
      return value;
    },
    setrtop(v, i) {
      let value = "";
      if (this.numm == 1) {
        if (i <= 2 && i > 0) {
          value = v - 50;
        }
        if (i == 3) {
          // alert(1);
          value = v - 50;
        }
        if (i > 3 && i <= 6) {
          value = v + 50;
        }
        if (i == 0) {
          value = v;
        }
      }
      if (this.numm == 2) {
        if (i <= 4 && i > 1) {
          value = v - 50;
        }
        if (i > 4 || i == 0) {
          value = v + 50;
        }
        if (i == 1) {
          value = v;
        }
      }
      if (this.numm == 3) {
        if (i <= 5 && i > 2) {
          value = v - 50;
        }
        if (i <= 1 || i == 6) {
          value = v + 50;
        }
        if (i == 2) {
          value = v;
        }
      }
      if (this.numm == 4) {
        if (i <= 6 && i > 3) {
          value = v - 50;
        }
        if (i <= 2) {
          value = v + 50;
        }
        if (i == 3) {
          value = v;
        }
      }
      if (this.numm == 5) {
        if (i == 0 || i >= 5) {
          value = v - 50;
        }
        if (i <= 3 && i > 0) {
          value = v + 50;
        }
        if (i == 4) {
          value = v;
        }
      }
      if (this.numm == 6) {
        if (i == 6 || i <= 1) {
          value = v - 50;
        }
        if (i <= 4 && i > 1) {
          value = v + 50;
        }
        if (i == 5) {
          value = v;
        }
      }
      if (this.numm == 7) {
        if (i <= 2) {
          value = v - 50;
        }
        if (i <= 5 && i > 2) {
          value = v + 50;
        }
        if (i == 6) {
          value = v;
        }
      }
      return value;
    },
    setoffleft(v, i) {
      let value = "";
      if (this.num == 1) {
        if (i <= 2) {
          value = v + 100;
        }
        if (i == 3) {
          value = v + 100;
        }
        if (i > 3 && i < 6) {
          value = v + 100;
        }
        if (i == 6) {
          value = v - 600;
        }
      }
      if (this.num == 2) {
        if (i <= 1 || i == 6) {
          value = v + 100;
        }
        if (i == 2) {
          value = v + 100;
        }
        if (i > 2 && i < 6) {
          value = v + 100;
        }
        if (i == 5) {
          value = v - 600;
        }
      }
      if (this.num == 3) {
        if (i > 4 || i == 0) {
          value = v + 100;
        }
        if (i == 1) {
          value = v + 100;
        }
        if (i >= 2 && i < 4) {
          value = v + 100;
        }
        if (i == 4) {
          value = v - 600;
        }
      }
      if (this.num == 4) {
        if (i <= 6 && i > 3) {
          value = v + 100;
        }
        if (i == 0) {
          value = v + 100;
        }
        if (i < 3 && i > 0) {
          value = v + 100;
        }
        if (i == 3) {
          value = v - 600;
        }
      }
      if (this.num == 5) {
        if (i >= 3 && i < 6) {
          value = v + 100;
        }
        if (i == 6) {
          value = v + 100;
        }
        if (i < 2) {
          value = v + 100;
        }
        if (i == 2) {
          value = v - 600;
        }
      }
      if (this.num == 6) {
        if (i >= 2 && i < 5) {
          value = v + 100;
        }
        if (i == 5) {
          value = v + 100;
        }
        if (i == 6 || i == 0) {
          value = v + 100;
        }
        if (i == 1) {
          value = v - 600;
        }
      }
      if (this.num == 7) {
        if (i > 0 && i < 4) {
          value = v + 100;
        }
        if (i == 4) {
          value = v + 100;
        }
        if (i > 4) {
          value = v + 100;
        }
        if (i == 0) {
          value = v - 600;
        }
      }
      return value;
    },
    setofftop(v, i) {
      let value = "";

      if (this.num == 1) {
        if (i <= 2) {
          value = v + 50;
        }
        if (i == 3) {
          // alert(1);
          value = v - 50;
        }
        if (i > 3 && i < 6) {
          value = v - 50;
        }
        if (i == 6) {
          value = v;
        }
      }
      if (this.num == 2) {
        if (i <= 1 || i == 6) {
          value = v + 50;
        }
        if (i == 2) {
          // alert(1);
          value = v - 50;
        }
        if (i > 2 && i < 5) {
          value = v - 50;
        }
        if (i == 5) {
          value = v;
        }
      }
      if (this.num == 3) {
        if (i > 4 || i == 0) {
          value = v + 50;
        }
        if (i == 1) {
          // alert(1);
          value = v - 50;
        }
        if (i >= 2 && i < 4) {
          value = v - 50;
        }
        if (i == 4) {
          value = v;
        }
      }
      if (this.num == 4) {
        if (i <= 6 && i > 3) {
          value = v + 50;
        }
        if (i == 0) {
          // alert(1);
          value = v - 50;
        }
        if (i < 3 && i > 0) {
          value = v - 50;
        }
        if (i == 3) {
          value = v;
        }
      }
      if (this.num == 5) {
        if (i >= 3 && i < 6) {
          value = v + 50;
        }
        if (i == 6) {
          // alert(1);
          value = v - 50;
        }
        if (i < 2) {
          value = v - 50;
        }
        if (i == 2) {
          value = v;
        }
      }
      if (this.num == 6) {
        if (i >= 2 && i < 5) {
          value = v + 50;
        }
        if (i == 5) {
          // alert(1);
          value = v - 50;
        }
        if (i == 6 || i == 0) {
          value = v - 50;
        }
        if (i == 1) {
          value = v;
        }
      }
      if (this.num == 7) {
        if (i > 0 && i < 4) {
          value = v + 50;
        }
        if (i == 4) {
          // alert(1);
          value = v - 50;
        }
        if (i > 4) {
          value = v - 50;
        }
        if (i == 0) {
          value = v;
        }
      }
      return value;
    },
  },
};
</script>

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
.box:nth-child(1) {
  left: 100px;
  top: 200px;
}
.box:nth-child(2) {
  left: 200px;
  top: 250px;
}
.box:nth-child(3) {
  left: 300px;
  top: 300px;
}
.box:nth-child(4) {
  left: 400px;
  top: 350px;
}
.box:nth-child(5) {
  left: 500px;
  top: 300px;
}
.box:nth-child(6) {
  left: 600px;
  top: 250px;
}
.box:nth-child(7) {
  left: 700px;
  top: 200px;
}
</style>