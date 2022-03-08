<template>
  <div id="app">
    <a-select
      mode="tags"
      style="width: 100%"
      placeholder="Tags Mode"
      @change="handleChange"
      @popupScroll="handleScroll"
    >
      <a-select-option v-for="i in list" :key="(i + 9).toString(36) + i">
        {{ i }}
      </a-select-option>
    </a-select>
  </div>
</template>

<script>
const list = Array.from(Array(10000), (c, i) => i + 1);
const pageSize = 20;

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      pageNum: 1,
    }
  },
  computed: {
    list() {
      return list.slice(0, this.pageNum * pageSize)
    }
  },
  methods: {
    handleChange(value) {
      console.log(`selected ${value}`);
    },
    handleScroll(e) {
      const { target } = e;
      // scrollHeight：代表包括当前不可见部分的元素的高度
      // scrollTop：代表当有滚动条时滚动条向下滚动的距离，也就是元素顶部被遮住的高度
      // clientHeight：包括padding但不包括border、水平滚动条、margin的元素的高度
      const rmHeight = target.scrollHeight - target.scrollTop;
      const clHeight = target.clientHeight;
      // 当下拉框失焦的时候，也就是不下拉的时候
      if (rmHeight === 0 && clHeight === 0) {
        // dispatchState({ type: 'stopScroll' });
      } else {
        console.log(rmHeight < clHeight + 5, rmHeight, clHeight, '=========')
        // 滚动到底部
        if (rmHeight < clHeight + 5) {
          // dispatchState({ type: 'scroll' });
          this.pageNum += 1
        }
      }
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
