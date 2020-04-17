<template>
  <div class="navbar">
    <hamburger
      id="hamburger-container"
      :is-active="sidebar.opened"
      class="hamburger-container"
      @toggleClick="toggleSideBar"
    />

    <breadcrumb id="breadcrumb-container" class="breadcrumb-container" />

    <div class="right-menu">
      <template v-if="device !== 'mobile'">
        <el-tooltip effect="dark" content="搜索" placement="bottom">
          <search id="header-search" class="right-menu-item" />
        </el-tooltip>
        <error-log class="errLog-container right-menu-item hover-effect" />

        <el-tooltip content="字体大小" effect="dark" placement="bottom">
          <size-select id="size-select" class="right-menu-item hover-effect" />
        </el-tooltip>
        <el-tooltip effect="dark" content="图表" placement="bottom">
          <Chart id="header-chart" class="right-menu-item" />
        </el-tooltip>
        <el-tooltip effect="dark" content="首页" placement="bottom">
          <Home id="header-home" class="right-menu-item" />
        </el-tooltip>
        <el-tooltip effect="dark" content="通知" placement="bottom">
          <Notice id="header-notice" class="right-menu-item" />
        </el-tooltip>
        <el-tooltip effect="dark" content="设置" placement="bottom">
          <HeadSet id="header-set" class="right-menu-item" />
        </el-tooltip>
      </template>

    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import Breadcrumb from "@/components/Breadcrumb";
import Hamburger from "@/components/Hamburger";
import ErrorLog from "@/components/ErrorLog";
import SizeSelect from "@/components/SizeSelect";
import Search from "@/components/HeaderSearch";
import Chart from "@/components/HeaderChart";
import Home from "@/components/HeaderHome";
import Notice from "@/components/HeaderNotice";
import HeadSet from "@/components/HeaderSet";

export default {
  components: {
    Breadcrumb,
    Hamburger,
    ErrorLog,
    SizeSelect,
    Search,
    Chart,
    Home,
    Notice,
    HeadSet
  },
  computed: {
    ...mapGetters(["sidebar", "avatar", "device"])
  },
  mounted(){
    console.log(this.sidebar)
  },
  methods: {
    toggleSideBar() {
      this.$store.dispatch("app/toggleSideBar");
    },
    async logout() {
      await this.$store.dispatch("user/logout");
      this.$router.push(`/login?redirect=${this.$route.fullPath}`);
    }
  }
};
</script>

<style lang="scss" scoped>
.navbar {
  height: 50px;
  overflow: hidden;
  position: relative;
  background: #fff;
  box-shadow: 0 1px 4px rgba(0, 21, 41, 0.08);

  .hamburger-container {
    line-height: 46px;
    height: 100%;
    float: left;
    cursor: pointer;
    transition: background 0.3s;
    -webkit-tap-highlight-color: transparent;

    &:hover {
      background: rgba(0, 0, 0, 0.025);
    }
  }

  .breadcrumb-container {
    float: left;
  }

  .errLog-container {
    display: inline-block;
    vertical-align: top;
  }

  .right-menu {
    float: right;
    height: 100%;
    line-height: 50px;

    &:focus {
      outline: none;
    }

    .right-menu-item {
      display: inline-block;
      padding: 0 8px;
      height: 100%;
      font-size: 18px;
      color: #5a5e66;
      vertical-align: text-bottom;

      &.hover-effect {
        cursor: pointer;
        transition: background 0.3s;

        &:hover {
          background: rgba(0, 0, 0, 0.025);
        }
      }
    }

    .avatar-container {
      margin-right: 30px;

      .avatar-wrapper {
        margin-top: 5px;
        position: relative;

        .user-avatar {
          cursor: pointer;
          width: 40px;
          height: 40px;
          border-radius: 10px;
        }

        .el-icon-caret-bottom {
          cursor: pointer;
          position: absolute;
          right: -20px;
          top: 25px;
          font-size: 12px;
        }
      }
    }
  }
}
</style>
