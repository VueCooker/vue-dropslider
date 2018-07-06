<template>
  <div id="app">
   <div class="movebox" >
    <div class="movego"></div>
    <div class="txt" id="txt">拖动滑块验证</div>
    <div class="move moveBefore" v-move></div>
  </div>
</div>
</template>

<script>
export default {
  name: 'vue-dropslider',
  props: ['dropsliderOptions'],
  data() {
    return {     
           
    }
  },
  directives: {
    move(el) {
        el.onmousedown = function(e) {
        var X = e.clientX - el.offsetLeft
        document.onmousemove = function(e) {
            var endx = e.clientX - X
        el.className = 'move moveBefore'
        el.style.left = endx + 'px'
       // console.log(el.parentNode.children[0])
        var width = document.querySelector('.movebox').offsetWidth - document.querySelector('.move').offsetWidth
         el.parentNode.children[0].style.width = endx + 'px'
         el.parentNode.children[1].innerHTML = '拖动滑块验证'
        //临界值小于
        if (endx <= 0) {
        el.style.left = 0 + 'px'
         el.parentNode.children[0].style.width = 0 + 'px'
        }
        //临界值大于
       // console.log(el.style.left)
        if (parseInt(el.style.left) >= width) {
        el.style.left = width + 'px'
         el.parentNode.children[0].style.width = width + 'px'
         el.parentNode.children[1].innerHTML = '验证通过'
        el.className = 'move moveSuccess'
        el.onmousedown = null
        }
        }
    }
    document.onmouseup = function() {
        document.onmousemove = null
    }
    }
  }
}

</script>

<style lang="scss" scoped>

.movebox{
    position: relative;
    background-color: #e8e8e8;
    width: 300px;
    height: 34px;
    line-height: 34px;
    text-align: center;
    .txt{
    position: absolute;
    top: 0px;
    width: 300px;
    -moz-user-select: none;
    -webkit-user-select: none;
    user-select: none;
    -o-user-select: none;
    -ms-user-select: none;
    }
    .movego{
      background-color: #7ac23c;
      height: 34px;
      width: 0px;
    }
      .move{
        position: absolute;
    top: 0px;
    left: 0px;
    width: 40px;
    height: 34px;
    border: 1px solid #ccc;
    cursor: move;
      }
      .moveBefore{
         background: #fff url("../assets/moveBefore.png") no-repeat center;
      }
      .moveSuccess{
         background: #fff url("../assets/moveSuccess.png") no-repeat center;
      }
    }
</style>
