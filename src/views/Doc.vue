<template>
  <div class="layout">
    <TopNav :toggle-menu-button-visible="true" class="nav"/>
    <div class="content">
      <aside v-if="menuVisible">
        <h2>开发指南</h2>
        <ol>
          <li>
            <router-link to="/doc/intro">介绍</router-link>
          </li>
          <li>
            <router-link to="/doc/install">安装</router-link>
          </li>
          <li>
            <router-link to="/doc/get-started">开始使用</router-link>
          </li>
        </ol>

        <h2>组件列表</h2>
        <ol>
          <li>
            <router-link to="/doc/switch">Switch 组件</router-link>
          </li>
          <li>
            <router-link to="/doc/button">Button 组件</router-link>
          </li>
          <li>
            <router-link to="/doc/input">Input 组件</router-link>
          </li>
          <li>
            <router-link to="/doc/dialog">Dialog 组件</router-link>
          </li>
          <li>
            <router-link to="/doc/tabs">Tabs 组件</router-link>
          </li>
          <li>
            <router-link to="/doc/icon">Icon 组件</router-link>
          </li>
          <li>
            <router-link to="/doc/radio">Radio 组件</router-link>
          </li>
          <li>
            <router-link to="/doc/message">Message 组件</router-link>
          </li>
          <li>
            <router-link to="/doc/popover">Popover 组件</router-link>
          </li>
          <li>
            <router-link to="/doc/layout">Layout 组件</router-link>
          </li>
          <li>
            <router-link to="/doc/grid">Grid 组件</router-link>
          </li>
          <li>
            <router-link to="/doc/collapse">Collapse 组件</router-link>
          </li>
          <li>
            <router-link to="/doc/pagination">Pagination 组件</router-link>
          </li>
          <li>
            <router-link to="/doc/slides">Slides 组件</router-link>
          </li>
          <li>
            <router-link to="/doc/cascader">Cascader 组件</router-link>
          </li>
        </ol>
      </aside>
      <main>
        <router-view/>
      </main>
    </div>
  </div>
</template>


<script lang="ts">
import TopNav from '../components/TopNav.vue';
import {inject, Ref} from 'vue';

export default {
  setup() {
    const menuVisible = inject<Ref<boolean>>('getChildren');
    return {menuVisible};
  },
  components: {
    TopNav
  },
};
</script>

<style lang="scss" scoped>
.layout {
  display: flex;
  flex-direction: column;
  height: 100vh;

  > .nav {
    flex-shrink: 0;
  }

  > .content {
    flex-grow: 1;
    padding-top: 60px;
    padding-left: 156px;
    @media (max-width: 500px) {
      padding-left: 0;
    }
  }
}

.content {
  display: flex;

  > aside {
    flex-shrink: 0;
    overflow: scroll;
    z-index: 5;
  }

  > main {
    flex-grow: 1;
    padding: 16px;
  }
}

aside {
  background: lightblue;
  width: 150px;
  padding: 16px 0;
  position: fixed;
  top: 0;
  left: 0;
  padding-top: 70px;
  height: 100%;
  z-index:1;

  > h2 {
    margin-bottom: 4px;
    padding: 0 16px;
  }

  > ol {
    > li {
      a {
        display: block;
        padding: 4px 16px;
        text-decoration: none;
      }

      > .router-link-active {
        background: white;
      }
    }
  }
}

main {
  overflow: auto;
}
</style>