<template>
  <div class="navbar">
    <hamburger :toggle-click="toggleSideBar" :is-active="sidebar.opened" class="hamburger-container"/>
    <breadcrumb />
    <div class="right-menu">
      <template v-if="device">
        <screenfull class="right-menu-item hover-effect" />
        <lang-select class="right-menu-item hover-effect" />
        <size-select class="right-menu-item hover-effect" />
      </template>
      <el-dropdown class="avatar-container right-menu-item hover-effect" trigger="click">
        <div class="avatar-wrapper">
          <!-- <img :src="avatar+'?imageView2/1/w/80/h/80'" class="user-avatar"> -->
          <img src="@/assets/understanding-flexbox-3.gif" class="user-avatar">
          <i class="el-icon-caret-bottom" />
        </div>
        <el-dropdown-menu slot="dropdown">
          <router-link to="/">
            <el-dropdown-item>
              {{ $t('navbar.dashboard') }}
            </el-dropdown-item>
          </router-link>
          <el-dropdown-item divided>
            <span style="display:block;" @click="logout">{{ $t('navbar.logOut') }}</span>
          </el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>
    </div>
  </div>
</template>

<script lang="ts">
import Breadcrumb from '@/components/Breadcrumb/index.vue'
import Hamburger from '@/components/Hamburger/index.vue'
import Screenfull from '@/components/Screenfull/index.vue'
import LangSelect from '@/components/LangSelect/index.vue'
import SizeSelect from '@/components/SizeSelect/index.vue'
import { Component, Vue } from 'vue-property-decorator'
import { AppModule } from '@/store/modules/app'
import { UserModule } from '@/store/modules/user'

@Component({
  components: {
    Breadcrumb,
    Hamburger,
    Screenfull,
    LangSelect,
    SizeSelect
  }
})
export default class Navbar extends Vue {
  get sidebar () {
    return AppModule.sidebar
  }
  get device () {
    return AppModule.device
  }

  get avatar () {
    return UserModule.avatar
  }

  private toggleSideBar () {
    AppModule.ToggleSideBar(false)
  }

  private logout () {
    UserModule.LogOut().then(() => {
      location.reload() // 为了重新实例化vue-router对象 避免bug
    })
  }
}
</script>

<style rel="stylesheet/scss" lang="sass" scoped>
.navbar
  height: 50px
  overflow: hidden
  box-shadow: 0 1px 3px 0 rgba(0,0,0,.12), 0 0 3px 0 rgba(0,0,0,.04)
  line-height: 50px
  .hamburger-container
    line-height: 46px
    height: 100%
    float: left
    cursor: pointer
    transition: background .3s
    &:hover
      background: rgba(0, 0, 0, .025)
  .breadcrumb-container
    float: left
  .errLog-container
    display: inline-block
    vertical-align: top
  .right-menu
    float: right
    height: 100%
    line-height: 50px
    &:focus
      outline: none
    .right-menu-item
      display: inline-block
      padding: 0 8px
      height: 100%
      font-size: 18px
      color: #5a5e66
      vertical-align: text-bottom
      &.hover-effect
        cursor: pointer
        transition: background .3s
        &:hover
          background: rgba(0, 0, 0, .025)
    .avatar-container
      margin-right: 30px
      .avatar-wrapper
        margin-top: 5px
        position: relative
        .user-avatar
          cursor: pointer
          width: 40px
          height: 40px
          border-radius: 10px
        .el-icon-caret-bottom
          cursor: pointer
          position: absolute
          right: -20px
          top: 25px
          font-size: 12px
</style>
