<script setup>
import Friends from '../.vitepress/theme/components/Friends.vue';

const friends = [
  {
    title: "十二",
    keywords: ["个人博客"],
    url: "https://blog.161122.xyz",
    description: "万里 の Blog",
    avatar: "https://blog.161122.xyz/assets/avatar.E6qFI8Ys.jpg",
  },
  {
    title: "Mlikiowa Home Village",
    keywords: ["个人博客"],
    url: "https://nanaeo.cn/",
    description: "A little Village With Mlikiowa",
    avatar: "https://q1.qlogo.cn/g?b=qq&nk=1627126029&s=100",
  },
  {
    title: "荒芜",
    keywords: ["个人博客"],
    url: "https://blog.a7bz.cn/",
    description: "记录分享一些笔记",
    avatar: "https://blog.a7bz.cn/logo.png"
  },
];
</script>

<Friends :friends="friends" />
