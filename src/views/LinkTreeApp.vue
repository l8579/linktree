<template>
  <div class="profile-wrapper">
    <div class="profile">
      <div class="profile-header">
        <img :src="avatar" alt="avatar" class="avatar" />
        <div class="profile-info">
          <div class="profile-header-info">
            <h3>{{ name }} <img src="../assets/checklist.png" alt="flag" class="flag" /></h3>
            <div class="profile-buttons">
              <a href="mailto:thanyanan.k8579@gmail.com" target="_blank" rel="noopener noreferrer">
                <p class="contact-btn">work contact email</p>
              </a>
            </div>
          </div>
          <div class="stats">
            <span>{{ posts }} posts</span>
            <span>{{ followers }} followers</span>
            <span>{{ favorites }} favorites</span>
          </div>
          <p>พิกัดรวมสินค้าและของใช้ทั้งหมด ✨</p>
          <div class="social-section">
            <div class="social-links">
              <div v-for="link in socialLinks" :key="link.name" class="social-link">
                <img :src="require(`@/assets/${link.icon}`)" :alt="link.name" />
                <!-- <span>{{ link.name }}</span> -->
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="tabs">
        <div v-for="tab in tabs" :key="tab" :class="['tab', { active: activeTab === tab }]" @click="activeTab = tab">
          {{ tab }}
        </div>
      </div>
      <div class="tab-content">
        <div v-if="activeTab === 'สกินแคร์'">
          <div class="image-grid">
            <div v-for="image in images1" :key="image.src" class="image-item">
              <a :href="image.link" target="_blank">
                <img :src="require(`@/assets/${image.src}`)" :alt="image.title" />
                <div class="image-title">{{ image.title }}</div>
              </a>
            </div>
          </div>
        </div>
        <div v-if="activeTab === 'อาหารเสริม'">
          <div class="image-grid">
            <div v-for="image in images2" :key="image.src" class="image-item">
              <a :href="image.link" target="_blank">
                <img :src="require(`@/assets/${image.src}`)" :alt="image.title" />
                <div class="image-title">{{ image.title }}</div>
              </a>
            </div>
          </div>
        </div>
        <div v-if="activeTab === 'ของกินอร่อยๆ'">
          <div class="image-grid">
            <div v-for="image in images3" :key="image.src" class="image-item">
              <a :href="image.link" target="_blank">
                <img :src="require(`@/assets/${image.src}`)" :alt="image.title" />
                <div class="image-title">{{ image.title }}</div>
              </a>
            </div>
          </div>
        </div>
        <div v-if="activeTab === 'ของใช้ ฯลฯ'">
          <div class="image-grid">
            <div v-for="image in images4" :key="image.src" class="image-item">
              <a :href="image.link" target="_blank">
                <img :src="require(`@/assets/${image.src}`)" :alt="image.title" />
                <div class="image-title">{{ image.title }}</div>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import socialLinks from '@/data/socialLinks.json';
import images1 from '@/data/images1.json';
import images2 from '@/data/images2.json';
import images3 from '@/data/images3.json';
import images4 from '@/data/images4.json';

export default {
  data() {
    return {
      name: "Papaya Salmon 🍣 ",
      posts: 60,
      followers: 15000,
      favorites: 200,
      avatar: require('@/assets/avatar.jpg'),
      socialLinks: socialLinks,
      tabs: ["สกินแคร์", "อาหารเสริม", "ของกินอร่อยๆ", "ของใช้ ฯลฯ"],
      activeTab: "สกินแคร์",
      images1: images1,
      images2: images2,
      images3: images3,
      images4: images4
    };
  }
};
</script>

<style>
.profile-wrapper {
  display: flex;
  width: 100%;
  height: 100vh;
  background: linear-gradient(to right, #6a11cb 25%, #f7797d 75%);
}

.profile {
  width: 50%;
  height: 90vh;
  margin: auto;
  background: white;
  padding: 20px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  border-radius: 15px;
}

.profile-header {
  display: flex;
  align-items: flex-start;
  margin-bottom: 20px;
}

.avatar {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  object-fit: cover;
  margin: 40px 50px;
}

.profile-info {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-top: 20px;
}

.profile-header-info {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.profile-buttons {
  display: flex;
  gap: 15px;
  /* margin-bottom: 10px; */
}

.profile-buttons a {
  color: #333;
  text-decoration: none;
}

.profile-info h3 {
  display: flex;
  align-items: center;
  font-weight: lighter;
  margin-right: 30px;
}

.flag {
  width: 20px;
  height: 20px;
  margin-left: 10px;
}

.follow-btn,
.contact-btn {
  background: #ebebeb;
  border-radius: 5px;
  padding: 5px 10px;
  margin: 5px 0;
  cursor: pointer;
  font-family: 'Kanit', sans-serif;
  font-weight: lighter;
}

.stats {
  display: flex;
  justify-content: space-around;
  margin: 0;
}

.stats span {
  font-weight: lighter;
  margin-right: 20px;
}

/* .social-section {
  margin-top: 10px;
} */

.social-links {
  display: flex;
  justify-content: space-around;
}

.social-link {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.social-link img {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  object-fit: cover;
  /* margin-top: 5px; */
  margin-right: 20px;
}

/* .social-link span {
  margin-top: 5px;
} */

.tabs {
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
  border-bottom: 1px solid #ccc;
}

.tab {
  padding: 10px 20px;
  cursor: pointer;
}

.tab.active {
  border-bottom: 2px solid black;
  font-weight: bold;
}

.tab-content {
  padding: 20px;
}

.image-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
  justify-content: center;
}

.image-item {
  width: calc(20% - 15px);
  box-sizing: border-box;
  border: 1px solid #e0e0e0;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.image-item:hover {
  transform: translateY(-5px);
}

.image-item img {
  width: 100%;
  height: auto;
  display: block;
}

.image-title {
  text-align: center;
  margin-top: 10px;
  font-weight: bold;
  color: #333;
  font-size: 1rem;
  font-weight: lighter;
}

.image-item a {
  text-decoration: none;
  color: inherit;
}

/* .image-item a:hover .image-title {
  color: #6a11cb;
} */
</style>