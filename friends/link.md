---
layout: page
title: 友链
aside: false
---

<script setup>
import Friends from '../.vitepress/theme/components/Friends.vue'

const friendsList = [
  {
    name: '十二',
    url: 'https://blog.161122.xyz/',
    avatar: 'https://blog.161122.xyz/assets/avatar.E6qFI8Ys.jpg',
    description: '万里 の Blog',
    tags: ['博客']
  },
  {
    name: 'Mlikiowa Home Village',
    url: 'https://nanaeo.cn/',
    avatar: 'https://q1.qlogo.cn/g?b=qq&nk=1627126029&s=100',
    description: 'A little Village With Mlikiowa',
    tags: ['博客']
  },
  {
    name: '荒芜',
    url: 'https://blog.a7bz.cn/',
    avatar: 'https://blog.a7bz.cn/logo.png',
    description: '记录分享一些笔记',
    tags: ['博客']
  }
]
</script>

<Friends type="list" :friends="friendsList" />
