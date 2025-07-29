<template>
  <div class="app-container">
    <div class="app-header">
      <header class="header">
        <h1>Усатая Няня — забота о вашем котике от Саиды</h1>
        <p>Пока вы в отпуске — ваш кот под надёжной защитой лап Саиды 🐾</p>
      </header>
    </div>

    <div class="benefits-block">
      <section class="section">
        <h2>Почему Саида?</h2>
        <div class="benefits-list">
          <div class="benefit-card">🐱 Опыт более 5 лет ухода за кошками всех возрастов и характеров</div>
          <div class="benefit-card">🏠 Уход на дому — минимальный стресс для вашего питомца</div>
          <div class="benefit-card">📷 Фотоотчёты и видео с котиком каждый день</div>
          <div class="benefit-card">💊 Поддержка при приёме лекарств и специальных диет</div>
          <div class="benefit-card">😻 Настоящая любовь к котикам и индивидуальный подход</div>
        </div>
      </section>
    </div>

    <div class="reviews-block">
      <section class="reviews">
        <h2>Отзывы довольных котиков</h2>
        <div class="slider" @touchstart="handleTouchStart" @touchend="handleTouchEnd">
          <div class="slider-track" :style="`transform: translateX(-${currentSlide * (isMobile ? 100 : 100 / 3)}%);`">
            <div
              v-for="(review, index) in reviews"
              :key="index"
              class="review-card"
            >
              <img :src="review.photo" alt="Фото котика" class="cat-photo" />
              <p class="review-text">"{{ review.text }}"</p>
              <p class="review-author">— {{ review.name }}, {{ review.age }}</p>
            </div>
          </div>
        </div>
        <div class="slider-dots">
          <button
            v-for="(_, index) in isMobile ? reviews.length : Math.ceil(reviews.length / 3)"
            :key="index"
            :class="['dot', { active: index === currentSlide }]"
            @click="currentSlide = index"
          ></button>
        </div>
      </section>
    </div>

    <div class="contact-block">
      <section class="section contact">
        <h2>Связаться с Саидой</h2>
        <form class="contact-form" @submit.prevent="handleSubmit">
          <input type="text" placeholder="Ваше имя" />
          <input type="email" placeholder="Email или Telegram" />
          <textarea placeholder="Коротко о вашем котике и датах отпуска"></textarea>
          <button type="submit">Отправить мяу</button>
        </form>
      </section>
    </div>

    <footer class="footer">
      &copy; 2025 Саида и довольные котики 🐾
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const currentSlide = ref(0)
const isMobile = ref(window.innerWidth < 768)
let touchStartX = 0
let touchEndX = 0

const handleResize = () => {
  isMobile.value = window.innerWidth < 768
}

onMounted(() => {
  window.addEventListener('resize', handleResize)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', handleResize)
})

const handleTouchStart = (e) => {
  touchStartX = e.changedTouches[0].screenX
}

const handleTouchEnd = (e) => {
  touchEndX = e.changedTouches[0].screenX
  handleSwipe()
}

const handleSwipe = () => {
  const minSwipeDistance = 50
  if (touchEndX < touchStartX - minSwipeDistance && isMobile.value && currentSlide.value < reviews.length - 1) {
    currentSlide.value++
  } else if (touchEndX > touchStartX + minSwipeDistance && isMobile.value && currentSlide.value > 0) {
    currentSlide.value--
  }
}

const handleSubmit = () => {
  alert('Саида обязательно с вами свяжется, как только проснётся и сделает потягушки 😺✨')
}

const reviews = [
  {
    name: 'Барсик',
    age: '7 лет',
    text: 'Мяу! Саида гладила меня ровно 37 минут в день — я засекал. Верните её!',
    photo: 'https://i.pinimg.com/736x/c8/a7/fd/c8a7fd5c874ee31f18354345e9caf553.jpg'
  },
  {
    name: 'Мурзя',
    age: '4 года',
    text: 'Миска всегда была полной. Лоток — чистым. Я думал, что снова родился.',
    photo: 'https://img.freepik.com/free-photo/adorable-white-cat-sunglasses-shirt-lies-fabric-hammock-ai-generated_268835-10929.jpg?semt=ais_hybrid&w=740'
  },
  {
    name: 'Клёпа',
    age: '9 лет',
    text: 'Саида понимала меня с полумяука. Теперь я сравниваю всех с ней...',
    photo: 'https://ornella.club/uploads/posts/2023-05/36589/1685200924_ornella-club-p-dovolnii-kotik-pinterest-1.jpg'
  },
  {
    name: 'Снежок',
    age: '1 год',
    text: 'Она приносила мне игрушки и чесала за ушком! 10/10!',
    photo: 'https://ornella.club/uploads/posts/2023-05/36589/1685200906_ornella-club-p-dovolnii-kotik-pinterest-7.jpg'
  },
  {
    name: 'Пуша',
    age: '5 лет',
    text: 'Мне пели колыбельные. Теперь я требую это от всех!',
    photo: 'https://storage.bankoboev.ru/big/7/big327930.jpg'
  },
  {
    name: 'Леопольд',
    age: '6 лет',
    text: 'Я боялся чужих, но Саида была как мама. Мяу-респект!',
    photo: 'https://img.freepik.com/premium-photo/pleased-with-gray-kitten-white-background-closed-his-eyes-portrait-scottish-cat_445280-6.jpg'
  }
]
</script>

<style>
body {
  margin: 0;
  font-family: 'Comic Sans MS', 'Segoe UI', sans-serif;
  background-color: #fffaf3;
  color: #4b2e2e;
  line-height: 1.5;
}

.app-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.app-header,
.benefits-block,
.reviews-block,
.contact-block {
  width: 100%;
  background-size: cover;
  background-position: center;
}

.header,
.section,
.reviews,
.contact {
  width: 100%;
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 20px;
  box-sizing: border-box;
}

.app-header {
  background-color: #fbd38d;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}

.header {
  padding: 30px;
  text-align: center;
}

.header h1 {
  margin: 0;
  font-size: 1.6rem;
  word-break: break-word;
}

.header p {
  font-style: italic;
  font-size: 1rem;
  margin-top: 10px;
  word-break: break-word;
}

.section {
  padding: 40px 0;
}

.section h2 {
  font-size: 1.4rem;
  margin-bottom: 20px;
  text-align: center;
  word-break: break-word;
}

.benefits-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 16px;
}

.benefit-card {
  flex: 1 1 100%;
  background: #fff;
  padding: 16px;
  text-align: center;
  border-radius: 8px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
  font-size: 0.9rem;
  word-wrap: break-word;
}

.reviews {
  text-align: center;
  padding: 40px 0;
}

.slider {
  overflow: hidden;
}

.slider-track {
  display: flex;
  transition: transform 0.5s ease;
}

.review-card {
  flex: 0 0 100%;
  max-width: 100%;
  padding: 20px;
  box-sizing: border-box;
  word-break: break-word;
  font-size: 0.9rem;
}

.review-card .cat-photo {
  width: 80px;
  height: 80px;
  object-fit: cover;
  border-radius: 50%;
  margin-bottom: 15px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.review-text {
  font-style: italic;
  margin-bottom: 8px;
  word-break: break-word;
}

.review-author {
  font-weight: bold;
  font-size: 0.85rem;
  word-break: break-word;
}

.slider-dots {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-top: 20px;
}

.dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background-color: #fbd38d;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.dot.active {
  background-color: #f6ad55;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 15px;
  max-width: 500px;
  margin: 0 auto;
  box-sizing: border-box;
}

.contact-form input,
.contact-form textarea {
  padding: 10px;
  border: 1px solid #f6ad55;
  border-radius: 6px;
  font-size: 1rem;
  word-break: break-word;
}

.contact-form button {
  background-color: #f6ad55;
  color: white;
  font-weight: bold;
  padding: 10px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.contact-form button:hover {
  background-color: #ed8936;
}

.footer {
  background-color: #fbd38d;
  padding: 20px;
  text-align: center;
  font-size: 0.9rem;
  margin-top: 40px;
  width: 100%;
  word-break: break-word;
  box-sizing: border-box;
}

@media (min-width: 768px) {
  .header h1 {
    font-size: 2.2rem;
  }

  .header p {
    font-size: 1.2rem;
  }

  .section h2 {
    font-size: 1.8rem;
  }

  .benefit-card {
    flex: 1 1 calc(30% - 16px);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }

  .benefit-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
  }

  .review-card {
    flex: 0 0 33.33%;
    max-width: 33.33%;
    font-size: 1rem;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }

  .review-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
  }

  .review-card .cat-photo {
    width: 100px;
    height: 100px;
  }
}
</style>



