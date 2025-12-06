<template>
  <div class="body">
    <!-- 导航栏 -->
    <div class="nav-container">
      <div class="nav">
        <div class="left">
          <span class="logo-text">TMK</span>
        </div>
        <div class="right">
          <ul>
            <li><a href="#" class="active">首页</a></li>
            <li><a href="#zp">作品</a></li>
            <li><a href="#bj">笔记</a></li>
            <li><a href="#ly">旅游</a></li>
            <li><router-link to="">关于</router-link></li>
          </ul>
        </div>
      </div>
    </div>

    <div class="center">
      <!-- Banner -->
      <div class="banner">
        <div class="banner-content">
          <h1>小凯的博客</h1>
          <p class="subtitle">记录生活，分享技术，探索世界</p>
          <!-- <p class="date">2025年12月6日</p> -->
        </div>
        <div class="banner-overlay"></div>
      </div>

      <!-- 作品 -->
      <section class="section-box" id="zp">
        <div class="section-header">
          <div class="header-left">
            <span class="section-title">精选作品</span>
            <span class="section-desc">Projects</span>
          </div>
          <router-link to="/works" class="more-link">查看更多 <span class="arrow">→</span></router-link>
        </div>
        <div class="scroll-container">
          <a :href="item.label" v-for="item in workslist" :key="item.id" class="card-link">
            <div class="card">
              <div class="card-img">
                <img src="../../assets/avatar.jpg" alt="封面">
                <div class="img-overlay"></div>
              </div>
              <div class="card-content">
                <h3 class="card-title">{{ item.title }}</h3>
                <div class="card-meta">
                  <div class="meta-item">
                    <svg class="icon" viewBox="0 0 1024 1024" width="14" height="14">
                      <path d="M512 73.143C269.605 73.143 73.143 269.605 73.143 512s196.462 438.857 438.857 438.857 438.857-196.462 438.857-438.857S754.395 73.143 512 73.143zm0-73.143c282.77 0 512 229.23 512 512s-229.23 512-512 512S0 794.77 0 512 229.23 0 512 0z" fill="#999"/>
                      <path d="M521.143 182.857c-25.234 0-45.714 20.48-45.714 45.714v320l-45.715 0a45.714 45.714 0 0 0 91.429 0V228.57c0-25.233-20.48-45.714-45.714-45.714z" fill="#999"/>
                      <path d="M523.337 507.611a45.714 45.714 0 0 0-32.292 78.044l165.778 160.548a45.714 45.714 0 0 0 64.622-64.585L555.666 521a45.568 45.568 0 0 0-32.33-13.385z" fill="#999"/>
                    </svg>
                    <span>{{ formatDate(item.time) }}</span>
                  </div>
                </div>
                <div class="card-tags">
                  <span class="tag">{{ item.technology || 'Tech' }}</span>
                </div>
              </div>
            </div>
          </a>
        </div>
      </section>

      <!-- 笔记 -->
      <section class="section-box" id="bj">
        <div class="section-header">
          <div class="header-left">
            <span class="section-title">学习笔记</span>
            <span class="section-desc">Notes</span>
          </div>
          <router-link to="/notes" class="more-link">查看更多 <span class="arrow">→</span></router-link>
        </div>
        <div class="scroll-container">
          <a :href="item.label" v-for="item in noteslist" :key="item.id" class="card-link">
            <div class="card note-card">
              <div class="card-content">
                <span class="note-icon">📝</span>
                <h3 class="card-title">{{ item.title }}</h3>
                <div class="card-meta">
                  <span>{{ formatDate(item.time) }}</span>
                </div>
                <div class="card-tags">
                  <span class="tag secondary">{{ item.technology || 'Note' }}</span>
                </div>
              </div>
            </div>
          </a>
        </div>
      </section>

      <!-- 旅游 -->
      <section class="section-box" id="ly">
        <div class="section-header">
          <div class="header-left">
            <span class="section-title">旅行足迹</span>
            <span class="section-desc">Travel</span>
          </div>
          <router-link to="/travel" class="more-link">查看更多 <span class="arrow">→</span></router-link>
        </div>
        <div class="scroll-container">
          <a :href="item.label" v-for="item in travellist" :key="item.id" class="card-link travel-link">
            <div class="card travel-card">
              <div class="card-img">
                <img :src="item.image" alt="风景">  <!-- use imageUrl -->
              </div>
              <div class = "travel-info">
              <h3 class="location">{{ item.name }}</h3>
              <p class="city">{{ item.city }}</p>
                <p class="station">{{ item.description }}</p>
                </div>
            </div>
          </a>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      workslist: [],
      noteslist: [],
      travellist: [],
      //travelList: [],  // change initial data
    }
  },
  methods: {
    // 简单的日期格式化辅助函数
    formatDate(dateStr) {
      if (!dateStr) return '';
      const date = new Date(dateStr);
      return `${date.getFullYear()}-${String(date.getMonth() + 1).padStart(2, '0')}-${String(date.getDate()).padStart(2, '0')}`;
    }
  },
  async created() {
    try {
      const res = await axios.get('http://47.79.40.65:3006');
      console.log("后端数据：", res.data);

      // 通用处理函数
      const processData = (data) => {
        if (data && Array.isArray(data)) {
          return data.sort((a, b) => new Date(b.time).getTime() - new Date(a.time).getTime()).slice(0, 4);
        }
        return [];
      };

      if (res.data) {
        this.workslist = processData(res.data.works);
        this.noteslist = processData(res.data.notes);
        this.travellist = processData(res.data.travel);
        // set up data from backend
        /* this.travellist = res.data.travel.map(item => ({
          id: item.id,          // Assuming the item has an 'id'
          name: item.location || "Unknown location", // show location as name
          city: item.city || "Unknown city",       // show city
          description: item.description || "No info",// station information
          imageUrl: item.imageUrl || "default-image-url.jpg" // image url, default image
        })); */
      }
    } catch (error) {
      console.error("请求失败:", error);
    }
  }
}
</script>

<style scoped>
/* 全局变量定义 */
:root {
  --primary-color: #3498db;            /* Main blue color */
  --secondary-color: #2ecc71;          /* Green accent */
  --accent-color: #e74c3c;            /* Red focus color */
  --bg-color: #f8f9fa;                /* Light background */
  --card-bg: #ffffff;                 /* Card background */
  --text-main: #34495e;               /* Dark gray text */
  --text-secondary: #7f8c8d;          /* Light gray text */
  --shadow-sm: 0 2px 4px rgba(0,0,0,0.05); /* Subtle shadow */
  --shadow-md: 0 4px 8px rgba(0,0,0,0.08); /* Medium shadow */
  --radius-lg: 12px;                 /* Large rounded corners */
  --radius-md: 8px;                  /* Medium rounded corners */
  --font-main: 'Nunito Sans', sans-serif;    /* Main font */
  --font-headers: 'Montserrat', sans-serif; /* Header font */
}

/* General styles */
body {
  font-family: var(--font-main);
  color: var(--text-main);
}

.body {
  width: 100%;
  min-height: 100vh;
  background-color: var(--bg-color);
  background-image: radial-gradient(#e1e1e1 1px, transparent 1px);
  background-size: 20px 20px;
  color: var(--text-main);
}

/* --- 导航栏 --- */
.nav-container {
  width: 100%;
  background: rgba(255, 255, 255, 0.9);
  /* backdrop-filter: blur(15px); */
  border-bottom: 1px solid rgba(0, 0, 0, 0.05);
  /* box-shadow: var(--shadow-sm); */
}

.nav {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  height: 70px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav .left .logo-text {
  font-size: 28px;                     /* Larger logo */
  font-weight: 700;
  color: var(--primary-color);          /* Use primary color */
  letter-spacing: -1px;
  font-family: var(--font-headers);      /* Distinct font for logo */
}

.nav .right ul {
  list-style: none;
  display: flex;
  gap: 30px;
  padding: 0;
  margin: 0;
}

.nav .right ul li a {
  text-decoration: none;
  color: var(--text-secondary);
  font-weight: 500;
  font-size: 16px;
  padding: 8px 0;
  position: relative;
  transition: color 0.3s;
}

.nav .right ul li a:hover,
.nav .right ul li a.active {
  color: var(--primary-color);
}

/* Navigation underline animation */
.nav .right ul li a::after {
  content: '';
  position: absolute;
  width: 0;
  height: 2px;
  bottom: 0;
  left: 0;
  background-color: var(--accent-color);
  transition: width 0.3s ease;
}

.nav .right ul li a:hover::after,
.nav .right ul li a.active::after {
  width: 100%;
}

/* --- 内容区域 --- */
.center {
  max-width: 1200px;
  margin: 0 auto;
  padding: 30px 20px 60px;
}

/* --- Banner --- */
.banner {
  width: 100%;
  height: 360px;
  border-radius: var(--radius-lg);
  margin-top: 20px;
  position: relative;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: white;
  box-shadow: var(--shadow-md);
  background: url(../../assets/avatar.jpg) center/cover no-repeat;
}

.banner-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(to bottom, rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.6));
  z-index: 1;
}

.banner-content {
  position: relative;
  z-index: 2;
  animation: fadeInUp 0.8s ease-out;
  padding: 20px;
}

.banner h1 {
  font-size: 56px;                 /* Increase font size */
  font-weight: 700;
  margin-bottom: 15px;
  letter-spacing: 2px;
  font-family: var(--font-headers); /* Use header font */
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3); /* Add shadow */
}

.banner .subtitle {
  font-size: 20px;                 /* Increase font size */
  opacity: 0.9;
  margin-bottom: 20px;
  font-weight: 300;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.3); /* Add subtle shadow */
}

/* --- 通用 Section --- */
.section-box {
  margin-top: 60px;
}

.section-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  margin-bottom: 25px;
  padding-bottom: 10px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.06);
}

.section-title {
  font-size: 32px;                 /* Larger title */
  font-weight: 700;
  color: var(--text-main);
  margin-right: 10px;
  font-family: var(--font-headers);
}

.section-desc {
  font-size: 14px;
  color: var(--text-secondary);
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.more-link {
  text-decoration: none;
  color: var(--text-secondary);
  font-size: 14px;
  display: flex;
  align-items: center;
  transition: all 0.3s;
}

.more-link:hover {
  color: var(--primary-color);
  transform: translateX(5px);
}

.more-link .arrow {
  margin-left: 5px;
  font-size: 16px;
}

/* --- 滚动容器 --- */
.scroll-container {
  display: flex;
  overflow-x: auto;
  gap: 25px;
  padding: 10px 5px 30px 5px;
  scrollbar-width: none;
  /* border: 1px solid red; */
}

/* --- 卡片通用样式 --- */
.card-link {
  text-decoration: none;
  color: inherit;
  flex: 0 0 300px;
  transition: transform 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
    border: 1px solid rgb(197, 196, 196);
    background-color: #fff;
    box-shadow:1px 20px 20px -2px rgb(197, 196, 196);
}

.card {
  background: var(--card-bg);
  border-radius: var(--radius-md);
  overflow: hidden;
  box-shadow: var(--shadow-sm);
  transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
  height: 100%;
  display: flex;
  flex-direction: column;
  border: 1px solid rgba(0, 0, 0, 0.03);
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-md);
}

.card-img {
  width: 100%;
  height: 200px;     /* Adjust the image size */
  overflow: hidden;
  /* position: relative; */
}

.card-img img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.travel-info {
  padding: 15px;           /* Adjust spacing inside the info */
}

.location {
  font-size: 18px;           /* Title/Location size */
  font-weight: bold;
  margin-bottom: 5px;
}

.city {
  color: var(--text-secondary);        /* City color */
  margin-bottom: 3px;
}
.station {
  font-size: 14px;
  color: var(--text-secondary);
  margin: 0px;
}

.card:hover .card-img img {
  transform: scale(1.05);
}

.card-content {
  padding: 20px;
  flex: 1;
  display: flex;
  flex-direction: column;
}

.card-title {
  font-size: 20px;                     /* Increase title size */
  font-weight: 600;
  margin: 0 0 10px 0;
  line-height: 1.4;
  color: var(--text-main);
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.card-meta {
  display: flex;
  align-items: center;
  color: var(--text-secondary);
  font-size: 13px;
  margin-bottom: 12px;
}

.meta-item {
  display: flex;
  align-items: center;
  gap: 6px;
}

.card-tags {
  margin-top: auto;
}

.tag {
  display: inline-block;
  background-color: rgba(52, 152, 219, 0.15); /* Lighter blue */
  color: var(--primary-color);           /* Primary color tag */
  padding: 6px 12px;                    /* Adjust padding */
  border-radius: 6px;
  font-size: 12px;
  font-weight: 500;
}

/* --- 笔记卡片特殊样式 --- */
.note-card {
    border: 1px solid rgb(197, 196, 196);
    background-color: #fff;
    box-shadow:1px 20px 20px -2px rgb(197, 196, 196);
  /* background: linear-gradient(145deg, #ffffff, #f0f0f0); */
  min-height: 200px;
}

.note-icon {
  font-size: 36px;
  margin-bottom: 15px;
  display: block;
  color: var(--secondary-color)         /* Green icon */
}

.tag.secondary {
  background-color: rgba(46, 204, 113, 0.15); /* Lighter green */
  color: var(--secondary-color);        /* Green tag */
}

/* --- 旅游卡片特殊样式 --- */
.travel-link {
  flex: 0 0 320px;
}

.travel-card {
    border: 1px solid rgb(197, 196, 196);
    background-color: #fff;
    box-shadow:1px 20px 20px -2px rgb(197, 196, 196);
  /* position: relative; */
  height: 350px; /* reduced height slightly*/
  display: flex;
  flex-direction: column;

}

.travel-info {
  padding: 15px; /* adjust the padding*/
  border-top: 1px solid rgba(0,0,0,0.05); /*Add a border*/
  flex-grow: 1;/* occupy remaining space*/
}

.travel-info h3 {
  font-size: 18px;
}

/* 动画定义 */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .nav-container {
    padding: 0 10px;
  }

  .nav .right ul {
    gap: 15px;
  }

  .nav .right ul li a {
    font-size: 14px;
  }

  .banner h1 {
    font-size: 40px;
  }

  .banner .subtitle {
    font-size: 16px;
  }

  .card-link {
    flex: 0 0 260px;
  }

  .section-title {
    font-size: 28px;
  }
}

@media (max-width: 576px) {
  .nav .left .logo-text {
    font-size: 24px;
  }

  .banner h1 {
    font-size: 32px;
  }

  .banner .subtitle {
    font-size: 14px;
  }

  .card-link {
    flex: 0 0 100%;
  }

  .scroll-container {
    padding-left: 0;
    padding-right: 0;
  }
}

/* Font imports */
/* @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@600&family=Nunito+Sans:wght@400;700&display=swap'); */
</style>
