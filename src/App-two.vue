<template>
  <div id="app">
    <a-select
      :value="value"
      style="width: 100%"
      placeholder="Tags Mode"
    >
      <template v-if="list.length">
        <div slot="dropdownRender" class="custom-dropdown">
          <RecycleScroller
            class="scroller"
            :items="list"
            key-field="id"
            :item-size="32"
          >
            <template slot-scope="{ item }">
              <li
                class="dropdown-item"
                @click="dropdownItemHandler(item)"
              >
                {{ item }}
              </li>
            </template>
          </RecycleScroller>
        </div>
      </template>
    </a-select>
  </div>
</template>

<script>
const list = Array.from(Array(10000), (c, i) => i + 1);
import 'vue-virtual-scroller/dist/vue-virtual-scroller.css';
import { RecycleScroller } from 'vue-virtual-scroller';

export default {
  name: 'App',
  components: {
    RecycleScroller,
  },
  data() {
    return {
      value: undefined,
      list: list,
    }
  },
  methods: {
    dropdownItemHandler(value) {
      console.log(`selected ${value}`);
      this.value = value;
    },
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
.custom-dropdown {
  height: 250px;
}
.custom-dropdown .scroller {
  height: 100%;
  overflow-y: scroll;
}
.custom-dropdown .dropdown-item {
  padding: 5px 12px;
  color: rgba(0, 0, 0, 0.65);
}
.custom-dropdown .dropdown-item:hover {
  background-color: #e6f7ff;
}
</style>
