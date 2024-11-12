<template>
  <div class="friends-container">
    <a
      v-for="(friend, index) in friends"
      :key="index"
      :href="friend.url"
      target="_blank"
      class="friend-card"
    >
      <div class="avatar">
        <img :src="friend.avatar" alt="Avatar" />
      </div>
      <div class="details">
        <h3 class="title">{{ friend.title }}</h3>
        <p class="keywords">
          <span v-for="(keyword, kIndex) in friend.keywords" :key="kIndex">
            {{ keyword }}
          </span>
        </p>
        <p class="description">{{ friend.description }}</p>
      </div>
    </a>
  </div>
</template>
  
<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  friends: {
    type: Array,
    required: true,
  },
});
</script>
  
<style scoped>
  a {
    text-decoration: none; /* Remove the underline */
  }
  
  .friends-container {
    display: grid; /* 使用 grid 布局 */
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr)); /* 自动适应卡片数量 */
    gap: 20px; /* 固定卡片间隔 */
    padding: 10px;
  }
  
  .friend-card {
    display: flex;
    flex-direction: row;
    padding: 15px;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    cursor: pointer;
    background-color: white;
    overflow: hidden;
    align-items: center; /* 垂直居中 */
    flex-shrink: 0;
  }

  .details {
    flex-grow: 1;
    max-width: calc(100% - 95px); /* 限制详情区域宽度，95px 是头像宽度 + 间距 */
    overflow: hidden;
  }

  .avatar {
    width: 80px;
    height: 80px;
    border-radius: 50%;
    overflow: hidden;
    margin-right: 15px; /* 头像和文字之间的间距 */
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .title {
    font-size: 20px;
    font-weight: bold;
  }

  .keywords {
    font-size: 12px;
    color: #777;
  }

  .description {
    font-size: 16px;
    color: #555;
    overflow: hidden;        /* 隐藏超出部分 */
    text-overflow: ellipsis; /* 使用省略号 */
    white-space: nowrap;     /* 不允许换行 */
  }
</style>
  