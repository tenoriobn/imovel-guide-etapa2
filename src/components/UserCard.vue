<template>
  <div class="card-container">
    <button class="user-card-container__color" @click="toggleBackgroundColor">
      <span class="colors" :style="{ backgroundColor: cardColor }"></span>
      <span class="colors color-secondary"></span>
    </button>

    <div class="user-card-container" :style="{ backgroundColor: cardBackgroundColor }">
      <div class="user-card-container__img" :style="{ borderColor: imgBorderColor }" >
        <img :src="image" v-if="image !== ''" alt="Foto de Perfil do User Card adicionada pelo usuário">
      </div>
      <div class="user-card-container__name">
        <h2>
          {{ name || 'Administrador' }}
          <span 
            :style="{ color: lastNameColor }">
            {{ surname || 'ImóvelGuide' }}
          </span>
        </h2>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      name: String,
      surname: String,
      image: String,
    },
    data() {
      return {
        cardBackgroundColor: 'var(--wine)',
        cardColor: 'var(--yellow)',
        lastNameColor: 'var(--wine)',
        imgBorderColor: 'var(--white)'
      };
    },
    methods: {
      toggleBackgroundColor() {
        this.cardBackgroundColor = this.cardBackgroundColor === 'var(--wine)' ? 'var(--yellow)' : 'var(--wine)';
        this.cardColor = this.cardColor === 'var(--yellow)' ? 'var(--wine)' : 'var(--yellow)';
        this.lastNameColor = this.lastNameColor === 'var(--yellow)' ? 'var(--wine)' : 'var(--yellow)';
        this.imgBorderColor = this.imgBorderColor === 'var(--white)' ? 'var(--black)' : 'var(--white)';
      },
    },
  };
</script>

<style scoped>
  .card-container {
    box-sizing: border-box;
    justify-self: center;
    width: 209px;
  }

  .user-card-container__color {
    display: flex;
    border: .125rem solid var(--gray);
    cursor: pointer;
    width: 40px;
    height: 24px;
    margin-bottom: 1.25rem;
    padding: 0;
  }

  .colors {
    display: block;
    width: 100%;
    height: 100%;
  }

  .color-primary {
    background-color: var(--yellow);
  }

  .color-secondary {
    background-color: var(--black);
  }

  .user-card-container {
    justify-self: center;
    display: grid;
    border: .125rem solid var(--gray);
    transition: background-color .3s ease-in-out;
  }

  .user-card-container__img {
    justify-self: center;
    display: block;
    box-sizing: border-box;
    border: .25rem solid var(--black);
    width: 116px;
    height: 120px;
    margin: 1.5rem 0;
  }

  .user-card-container__img img {
    object-fit: cover;
    width: 100%;
    height: 100%;
  }

  .user-card-container__name {
    box-sizing: border-box;
    background-color: var(--black);
    border-top: .125rem solid var(--gray);
    padding: .5rem;
    max-width: 205px;
  }

  .user-card-container__name h2, 
  .user-card-container__name span {
    color: var(--white);
    font-size: .75rem;
    font-weight: 500;
    text-align: center;
    text-transform: uppercase;
    white-space: wrap;
    overflow: hidden;
    text-overflow: ellipsis;
    transition: color .3s ease-in-out;
  }
</style>