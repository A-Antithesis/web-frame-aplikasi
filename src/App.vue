<template>
  <div id="app">
    <header class="app-header">
      <h1>APLIKASI CLICKER ANIME</h1>
    </header>
    
    <div class="main-content">
      <section class="card counter-card">
        <h2>Counter Count</h2>
        <p class="count-display">Count: {{ count }}</p>
        <div class="button-container">
          <button @click="decrementCount" aria-label="Decrement Count" class="counter-button">
            &#8722;
          </button>
          <button @click="incrementCount" aria-label="Increment Count" class="counter-button">
            &#43;
          </button>
        </div>
        <div class="popcat-animation">
          <img :src="popcatImage" alt="Popcat Animation" />
        </div>
      </section>

      <section class="card color-card">
        <h2>Color Box</h2>
        <div :style="{ backgroundColor: boxColor }" class="color-box" aria-label="Color Box"></div>
        <div class="color-picker-container">
          <input type="color" v-model="boxColor" class="color-picker" aria-label="Pick Color"/>
          <button @click="changeColor" aria-label="Change Color" class="color-button">
            Update Color
          </button>
        </div>
      </section>

      <section class="card carousel-card">
        <h2>Image Carousel</h2>
        <div class="carousel">
          <img 
            :src="images[currentImage]" 
            :alt="`Carousel image ${currentImage + 1}`" 
            class="carousel-image"
          />
          <div class="button-container carousel-buttons">
            <button @click="prevImage" aria-label="Previous Image" class="carousel-button">
              &#10094;
            </button>
            <button @click="nextImage" aria-label="Next Image" class="carousel-button">
              &#10095;
            </button>
          </div>
        </div>
        <p class="image-info">Image {{ currentImage + 1 }} of {{ images.length }}</p>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      count: 0,
      boxColor: '#ffcccb',
      images: [
        'https://rb.gy/nuh8v5',
        'https://shorturl.at/pbLpn',
        'https://shorturl.at/5QzUo',
        'https://shorturl.at/VRSWi',
        'https://rb.gy/v7cox4',
      ],
      currentImage: 0,
      popcatImages: [
        'https://rb.gy/58p0r8',
        'https://rb.gy/522mzh'
      ],
      popcatImage: 'https://shorturl.at/0P9l0',
    };
  },
  methods: {
    incrementCount() {
      this.count++;
      this.updatePopcatImage();
    },
    decrementCount() {
      if (this.count > 0) this.count--;
      this.updatePopcatImage();
    },
    updatePopcatImage() {
      this.popcatImage = this.popcatImages[this.count % this.popcatImages.length];
    },
    changeColor() {
      const randomColor = `#${Math.floor(Math.random() * 16777215).toString(16)}`;
      this.boxColor = randomColor;
    },
    nextImage() {
      this.currentImage = (this.currentImage + 1) % this.images.length;
    },
    prevImage() {
      this.currentImage = (this.currentImage - 1 + this.images.length) % this.images.length;
    }
  }
}
</script>

<style>
:root {
  --color-background: #f4f4f4;
  --color-text: #333;
  --color-card: #fff;
  --color-border: #6498e6;
  --color-primary: #4c8bbe;
}

html, body {
  height: 100%;
  margin: 0;
  padding: 0;
  font-family: 'Arial', sans-serif;
  background-image: url('https://shorturl.at/5ElIC'); /* Ganti dengan URL gambar yang diinginkan */
  background-size: cover; /* Menutup seluruh area */
  background-repeat: no-repeat; /* Menghindari pengulangan gambar */
  background-position: center; /* Memusatkan gambar */
}

#app {
  text-align: center;
  background-color: var(--color-background);
  padding: 20px;
  background-color: rgba(255, 255, 255, 0); /* Warna latar belakang dengan transparansi */
  overflow-y: auto;
}

.app-header {
  background-color: var(--color-primary);
  color: white;
  padding: 20px 0;
  position: sticky;
  top: 0;
}

.main-content {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 20px;
}

.card {
  background-color: var(--color-card);
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  padding: 20px;
  border: 1px solid var(--color-border);
  flex: 1;
  min-width: 300px;
}

.count-display {
  font-size: 1.5rem;
  font-weight: bold;
}

.color-box {
  width: 100%;
  height: 200px;
  margin: 10px auto;
  border-radius: 10px;
  border: 1px solid var(--color-border);
}

.button-container {
  display: flex;
  justify-content: center;
  gap: 15px;
}

.color-button {
  background-color: var(--color-primary);
  color: white;
  border: none;
  padding: 10px 15px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.color-button:hover {
  background-color: #45a049;
}

.carousel {
  position: relative;
}

.carousel-image {
  max-width: 100%;
  border-radius: 10px;
}

.carousel-button {
  padding: 10px;
  border: none;
  border-radius: 50%;
  cursor: pointer;
  background-color: var(--color-primary);
  color: white;
  transition: background-color 0.3s;
}

.carousel-button:hover {
  background-color: #45a049;
}

.image-info {
  margin-top: 10px;
  font-weight: bold;
}

.popcat-animation img {
  max-width: 150px;
  height: auto;
}
</style>