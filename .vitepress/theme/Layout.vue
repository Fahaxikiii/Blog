<template>
  <Splash></Splash>
  <template v-if="!page.isNotFound">
    <main :class="{ 'friends-page': page.filePath?.includes('friends/') }" style="min-height: 100vh">
      <Navbar></Navbar>
      <Banner>
        <transition name="fade" mode="out-in">
          <WelcomeBox v-if="!state.splashLoading && page.filePath === 'index.md'"></WelcomeBox>
          <Tags v-else-if="page.filePath === 'tags/index.md'"></Tags>
          <div class="friends-banner" v-else-if="page.filePath?.includes('friends/')"></div>
          <PostInnerBanner v-else></PostInnerBanner>
        </transition>
      </Banner>
      <div class="content-area" :class="{ 'friends-content': page.filePath?.includes('friends/') }">
        <transition name="fade" mode="out-in">
          <PostsList
            v-if="page.filePath === 'index.md' || page.filePath === 'tags/index.md'"
          ></PostsList>
          <PostViewer v-else-if="!page.filePath?.includes('friends/')"></PostViewer>
          <div class="friends-wrapper" v-else>
            <Content />
          </div>
        </transition>
      </div>
    </main>
    <Footer></Footer>
    <Fireworks v-if="state.fireworksEnabled"></Fireworks>
    <ToTop></ToTop>
  </template>
  <NotFound v-else></NotFound>
</template>

<script setup lang="ts">
// 组件导入
import Splash from './components/Splash.vue'
import Navbar from './components/Navbar/index.vue'
import Banner from './components/Banner.vue'
import WelcomeBox from './components/Welcome-Box.vue'
import PostsList from './components/Posts-List.vue'
import Tags from './components/Tags.vue'
import PostViewer from './components/Post-Viewer.vue'
import PostInnerBanner from './components/Post-InnerBanner.vue'
import NotFound from './components/NotFound.vue'
import ToTop from './components/ToTop.vue'
import Fireworks from './components/Fireworks.vue'
import Footer from './components/Footer.vue'
// 路径切换
import { useData } from 'vitepress'
const { page } = useData()

import { useStore } from './store'
const { state } = useStore()
</script>

<style lang="less">
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

html {
  scroll-behavior: smooth;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

body {
  background-image: url('./assets/background.svg');
  background-color: var(--general-background-color);
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  background-attachment: fixed;
  overflow-y: scroll;
  overflow-x: hidden;
  color: var(--font-color-grey);
  font-family: 'Blueaka', sans-serif;
}

ul {
  list-style: none;
}

a {
  text-decoration: none;
}

::-webkit-scrollbar {
  width: 6px;
  height: 6px;
}

::-webkit-scrollbar-thumb {
  border-radius: 3px;
  background: var(--color-blue);
  cursor: pointer;
}

.friends-page {
  position: relative;
  
  .content-area {
    position: relative;
    z-index: 10;
  }
}

.friends-banner {
  height: 40vh;
}

.friends-wrapper {
  width: 100%;
  padding-top: calc(40vh - 360px);
  position: relative;
  z-index: 51;
  min-height: 100vh;
  background: linear-gradient(
    to bottom,
    transparent,
    var(--general-background-color) 50%
  );
}

.friends-content {
  margin-top: -40vh;
}
</style>
