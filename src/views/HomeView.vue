<script setup>
import { ref, onMounted } from 'vue'; // Импортируем необходимые функции
import TheHeader from '../components/TheHeader.vue';
import TheContent from '@/components/TheContent.vue';
import TheFooter from '@/components/TheFooter.vue';

// Создаем реактивную переменную для высоты окна
const windowHeight = ref(null);

onMounted(() => {
  // Устанавливаем высоту окна при первой загрузке
  windowHeight.value = window.innerHeight;
  const footer = document.querySelector('.container');
  if (footer) {
    footer.style.display = 'none';
  }
});
</script>

<template>
  <header>
    <TheHeader />
  </header>
  <main>
    <section class="scontent" :style="{
      height: windowHeight + 'px'
    }">
      <TheContent />
    </section>
  </main>
  <footer>
    <TheFooter />
  </footer>
</template>
