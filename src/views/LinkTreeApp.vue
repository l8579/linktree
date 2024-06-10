<template>
  <div class="profile-wrapper">
    <transition name="fade">
      <div class="profile" v-if="loaded">
        <div class="profile-header">
          <img :src="avatar" alt="avatar" class="avatar" />
          <div class="profile-info">
            <div class="profile-header-info">
              <h3>{{ name }} <img src="../assets/checklist.png" alt="flag" class="flag" /></h3>
              <div class="profile-buttons"></div>
            </div>
            <div class="stats">
              <span>{{ animatedPosts }} posts</span>
              <span>{{ animatedFollowers }} followers</span>
              <span>{{ animatedFavorites }} favorites</span>
            </div>
            <p>พิกัดรวมสินค้าและของใช้ทั้งหมด ✨</p>
            <div class="social-section">
              <div class="social-links">
                <div v-for="link in socialLinks" :key="link.name" class="social-link">
                  <a :href="link.link" target="_blank" rel="noopener noreferrer">
                    <img :src="require(`@/assets/${link.icon}`)" :alt="link.name" />
                  </a>
                </div>
                <a href="mailto:thanyanan.k8579@gmail.com" target="_blank" rel="noopener noreferrer" class="aZzz">
                  <p class="contact-btn">work contact email</p>
                </a>
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
          <div v-if="activeTab === 'ของใช้ เสื้อผ้า ฯลฯ'">
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
    </transition>
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
      tabs: ["สกินแคร์", "อาหารเสริม", "ของกินอร่อยๆ", "ของใช้ เสื้อผ้า ฯลฯ"],
      activeTab: "สกินแคร์",
      images1: images1,
      images2: images2,
      images3: images3,
      images4: images4,
      loaded: false,
      animatedPosts: 0,
      animatedFollowers: 0,
      animatedFavorites: 0
    };
  },
  mounted() {
    this.loaded = true;
    this.animateNumber('animatedPosts', this.posts, 2000);
    this.animateNumber('animatedFollowers', this.followers, 2000);
    this.animateNumber('animatedFavorites', this.favorites, 2000);
  },
  methods: {
    animateNumber(ref, value, duration) {
      let start = 0;
      let increment = value / (duration / 16); // 16 ms for each frame (60fps)
      const animate = () => {
        start += increment;
        if (start >= value) {
          this[ref] = value;
        } else {
          this[ref] = Math.floor(start);
          requestAnimationFrame(animate);
        }
      };
      animate();
    }
  }
};
</script>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

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
  /* margin-bottom: 10px; */
}

.profile-buttons {
  display: flex;
  gap: 15px;
  /* margin-bottom: 10px; */
}

.profile-info .aZzz {
  color: #333;
  text-decoration: none;
  margin-top: -5px;
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
  justify-content: flex-start;
  overflow-y: auto;
  height: 550px;
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

/* Media Queries */

/* Mobile Devices */
@media only screen and (max-width: 600px) {
  .profile {
    width: 90%;
    height: auto;
    margin: 20px auto;
  }

  .avatar {
    display: none;
  }

  .profile-info {
    margin-top: 0;
    font-size: 0.8rem;
  }

  .image-grid {
    height: 550px;
  }

  .image-item {
    width: calc(50% - 15px);
  }

  .image-title {
    font-size: 0.8rem;
    height: 30px;
  }

  .tab-content {
    padding: 10px 0;
  }

  .tabs {
    font-size: 0.5rem;
  }

  .tab {
    padding: 10px 0;
  }
}

/* Tablets */
@media only screen and (min-width: 600px) and (max-width: 768px) {
  .profile {
    width: 90%;
    height: auto;
    margin: 20px auto;
  }

  .avatar {
    width: 120px;
    height: 120px;
    /* margin: 20px 0; */
    margin: 40px 30px;
  }

  .image-item {
    width: calc(33.33% - 15px);
  }

  .image-title {
    height: 35px;
  }

  .image-grid {
    height: 480px;
  }
}

/* Small Desktops */
@media only screen and (min-width: 768px) and (max-width: 1024px) {
  .profile {
    width: 90%;
    height: auto;
    margin: 20px auto;
  }

  .avatar {
    width: 120px;
    height: 120px;
    /* margin: 20px 0; */
    margin: 40px 50px;
  }

  .image-item {
    width: calc(33.33% - 15px);
  }

  .image-title {
    height: 35px;
  }

  .image-grid {
    height: 500px;
  }
}

/* Medium Desktops */
@media only screen and (min-width: 1024px) and (max-width: 1280px) {
  .profile {
    width: 80%;
    height: auto;
    margin: 20px auto;
  }

  .avatar {
    width: 120px;
    height: 120px;
    /* margin: 20px 0; */
    margin: 40px 50px;
  }

  .image-item {
    width: calc(25% - 15px);
  }

  .image-title {
    height: 40px;
  }

  .image-grid {
    height: 500px;
  }
}

/* Large Desktops */
@media only screen and (min-width: 1281px) and (max-width: 2000px) {
  .profile {
    width: 50%;
    height: auto;
    margin: 20px auto;
  }

  .avatar {
    width: 140px;
    height: 140px;
    margin: 30px 40px;
    /* margin: 40px 50px; */
  }

  .profile-info {
    margin-top: 10px;
  }

  .image-item {
    width: calc(25% - 15px);
  }

  .image-grid {
    height: 500px;
  }

  .image-title {
    text-align: center;
    margin-top: 10px;
    color: #333;
    height: 40px;
    font-size: 1rem;
    font-weight: lighter;
  }
}

/* Large Desktops */
@media only screen and (min-width: 2560px) {
  .profile {
    width: 50%;
    height: auto;
    margin: 20px auto;
  }

  .avatar {
    width: 180px;
    height: 180px;
    margin: 40px 50px;
    /* margin: 40px 50px; */
  }

  .profile-info {
    margin-top: 10px;
    font-size: 1.5rem;
  }

  .social-link img {
    width: 50px;
    height: 50px;
  }

  .profile-info .aZzz {
    margin-top: 0px;
    margin-left: 5px;
  }

  .image-grid {
    height: 950px;
  }

  .image-item {
    width: calc(25% - 15px);
  }

  .image-title {
    font-size: 1.8rem;
    height: 60px;
  }

  .tabs {
    font-size: 1.6rem;
  }
}
</style>