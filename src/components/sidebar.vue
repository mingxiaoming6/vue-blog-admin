<template>
  <el-menu
    :default-active="defaultPage"
    :unique-opened=true
    :collapse="isCollapse"
    class="el-menu-sidebar"
    background-color="#1f2d3d"
    text-color="#fff"
    active-text-color="#1890ff"
    @select="activeMenu"
    router
  >
    <el-menu-item class="menu-sidebar-head">
      <span slot="title">vue-blog-admin</span>
    </el-menu-item>
    <template v-for="menu in sideMenu">
      <el-submenu
        v-if="menu.children && menu.children.length !== 0"
        :index="menu.path"
        :key="menu.path"
      >
        <template slot="title">
          <i :class="menu.icon"></i>
          <span slot="title">{{ menu.label }}</span>
        </template>
        <el-menu-item
          v-for="childMenu in menu.children"
          :key="childMenu.path"
          :index="childMenu.path"
        >
          <i :class="childMenu.icon"></i>
          <span slot="title">{{ childMenu.label }}</span>
        </el-menu-item>
      </el-submenu>
      <el-menu-item
        v-else
        :index="menu.path"
        :key="menu.path"
        @click="activePage(menu)"
      >
        <i :class="menu.icon"></i>
        <span slot="title">{{ menu.label }}</span>
      </el-menu-item>
    </template>
  </el-menu>
</template>

<script>
export default {
  name: 'sidebar',
  props: {
    isCollapse: {
      type: Boolean,
      default: false
    },
    routerPath: {
      type: String,
      default: '/main-view/home-page'
    }
  },
  watch: {
    routerPath: {
      handler(val) {
        this.defaultPage = val;
      },
      deep: true
    },
    $route() {
      this.defaultPage = window.location.pathname;
    }
  },
  mounted() {
    this.defaultPage = window.location.pathname;
  },
  data() {
    return {
      defaultPage: '',
      sideMenu: [
        {
          icon: 'el-icon-data-analysis',
          label: '首页',
          path: '/main-view/home-page'
        },
        {
          icon: 'el-icon-user',
          label: '用户管理',
          path: '/main-view/user-manage'
        },
        {
          icon: 'el-icon-notebook-1',
          label: '博客管理',
          path: '/main-view/blog-manage'
        }
      ],
      allOpenPage: [{
        icon: 'el-icon-data-analysis',
        label: '首页',
        path: '/main-view/home-page'
      }]
    }
  },
  methods: {
    /**
     * 路由跳转
     */
    activeMenu(index, indexPath) {
      this.$store.commit('defaultMenu', index);
      sessionStorage.setItem('state', JSON.stringify(this.$store.state));
    },
    /**
     * 保存已打开页面到vuex中
     */
    activePage(menu) {
      if(menu.label === '首页') { return }
      if(this.allOpenPage.indexOf(menu) === -1) {
        this.allOpenPage.push(menu);
      }
      this.$store.commit('allOpenPage', this.allOpenPage);
    }
  }
}
</script>

<style lang="scss">
.el-menu-sidebar {
  height: 100%;
  .menu-sidebar-head{
    height: 60px;
    line-height: 60px;
    margin-bottom: 2px;
    &:hover {
      background: transparent;
    }
  }
}
</style>