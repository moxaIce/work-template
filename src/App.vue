<script setup>
import {reactive, shallowRef} from "vue";
import UxUpdate from './components/ux-update.vue';
import Test from './components/test.vue'
const defaultCurrentMenu = {
  name: 'ux-update-2.0',
  component: UxUpdate
}

const menus = reactive({
  list: [
    defaultCurrentMenu,
    {
      name: 'test',
      component: Test
    }
  ]
})
const currentComponent = shallowRef(JSON.parse(JSON.stringify(defaultCurrentMenu)))

const updateComponents = (item) => {
  Object.assign(currentComponent, item)

}
</script>

<template>
  <div class="root">
    <el-menu active-text-color="#ffd04b"
             background-color="#545c64"
             class="el-menu-vertical-demo"
             default-active="2"
             text-color="#fff">
      <el-menu-item v-for="(item, index) in menus.list" @click="updateComponents(item)" :key="index">
        {{ item.name }}
      </el-menu-item>
    </el-menu>
    <component :is="currentComponent.component"></component>
  </div>
</template>

<style scoped>
.root{
  display: flex;
  width: 100vw;
  height: 100vh;
}
</style>
