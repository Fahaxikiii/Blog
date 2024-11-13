<script setup lang="ts">
import { computed, onMounted, ref } from 'vue'

const openUrl = (url: string) => window?.open(url, '_blank')

interface Friend {
  name: string
  avatar: string
  url: string
  description: string
  tags?: string[]
}

const props = defineProps({
  type: {
    type: String,
    default: 'list'
  },
  friends: {
    type: Array as () => Friend[],
    required: true
  }
})

const containerRef = ref<HTMLElement | null>(null)

onMounted(() => {
  if (containerRef.value) {
    const height = containerRef.value.offsetHeight
    document.documentElement.style.setProperty('--friends-content-height', `${height}px`)
  }
})
</script>

<template>
  <div class="friends-container" ref="containerRef">
    <div class="friends-list">
      <div v-for="friend in friends" :key="friend.name" class="friend-card" @click="openUrl(friend.url)">
        <div class="card-inner">
          <div class="card-front">
            <div class="friend-avatar">
              <img :src="friend.avatar" :alt="friend.name">
            </div>
            <div class="friend-info">
              <div class="friend-header">
                <h3 class="friend-name">{{ friend.name }}</h3>
                <div class="friend-tags">
                  <span v-for="tag in friend.tags" :key="tag" class="tag">{{ tag }}</span>
                </div>
              </div>
              <p class="friend-description">{{ friend.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="less">
.friends-container {
  width: 90%;
  max-width: 1400px;
  margin: 0 auto;
  padding: 20px;
  box-sizing: border-box;
  position: relative;
  z-index: 52;
}

.friends-list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  width: 100%;
}

.friend-card {
  background: rgba(0, 255, 255, 0.15);
  border-radius: 16px;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  overflow: hidden;
  transition: all 0.3s ease;
  cursor: pointer;
  position: relative;
  z-index: 53;

  &:hover {
    transform: translateY(-5px);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
    background: rgba(0, 255, 128, 0.2);
    z-index: 54;
  }
}

.card-inner {
  padding: 20px;
}

.card-front {
  display: flex;
  gap: 20px;
}

.friend-avatar {
  flex-shrink: 0;
  width: 80px;
  height: 80px;
  border-radius: 50%;
  overflow: hidden;
  border: 2px solid rgba(255, 255, 255, 0.5);

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.3s ease;
  }

  &:hover img {
    transform: scale(1.1);
  }
}

.friend-info {
  flex: 1;
  min-width: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.friend-header {
  margin-bottom: 10px;
}

.friend-name {
  margin: 0;
  font-size: 1.2em;
  color: var(--font-color-gold);
  margin-bottom: 8px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.friend-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.tag {
  padding: 2px 8px;
  font-size: 0.8em;
  color: var(--font-color-gold);
  background: rgba(0, 255, 255, 0.2);
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.3);
}

.friend-description {
  margin: 0;
  font-size: 0.9em;
  color: var(--font-color-grey);
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  line-height: 1.4;
}

@media (min-width: 1600px) {
  .friends-list {
    grid-template-columns: repeat(4, 1fr);
  }
}

@media (max-width: 1599px) and (min-width: 1200px) {
  .friends-list {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media (max-width: 1199px) and (min-width: 768px) {
  .friends-list {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 767px) {
  .friends-container {
    width: 95%;
    padding: 15px;
    position: relative;
  }

  .friends-list {
    grid-template-columns: 1fr;
    gap: 15px;
  }

  .friend-avatar {
    width: 60px;
    height: 60px;
  }

  .card-inner {
    padding: 15px;
  }

  .friend-name {
    font-size: 1.1em;
  }

  .friend-description {
    font-size: 0.85em;
  }
}

@media (max-width: 480px) {
  .friends-container {
    width: 92%;
    padding: 10px;
    position: relative;
  }

  .card-inner {
    padding: 12px;
  }

  .friend-avatar {
    width: 50px;
    height: 50px;
  }

  .card-front {
    gap: 12px;
  }

  .friend-name {
    font-size: 1em;
  }

  .tag {
    padding: 1px 6px;
    font-size: 0.75em;
  }
}
</style> 