<template>
  <div class="card">
    <a :href="anime.url" class="card__link" target="_blank">
      <img :src="anime.images.jpg.image_url" alt="Anime" />
      <h3 class="card__title">{{ anime.title }}</h3>
    </a>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: ['anime'],
}
</script>

<style lang="scss" scoped>
.card {
  flex: 1 1 33%;
  width: 33%;
  max-width: 33%;
  padding: 0 8px;
  margin-bottom: 16px;

  img {
    width: 100%;
    height: 300px;
    object-fit: cover;
    border-radius: 16px;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.15);
    transition: 0.4s;
  }
  h3 {
    padding: 16px;
    text-align: center;
    color: #313131;
    transition: 0.4s;
  }

  &:hover {
    img {
      transform: scale(1.1);
    }

    h3 {
      color: green;
    }
  }
}
</style>
