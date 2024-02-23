<template>
  <div class="user-panel-container">
    <div class="user-profile-container">
      <div class="user-profile-container__img">
        <img :src="imageSrc" v-if="imageSrc !== ''" alt="Foto de perfil selecionada pelo usuário para o User Card">
      </div>
      <button type="button" class="add-photo-btn" @click="openFileUpload">Adicionar Foto</button>
      <input
        id="file-upload"
        type="file"
        style="display: none"
        @change="handleImageUpload"
        ref="fileInput"
      />
    </div>

    <form class="user-form-container">
      <div class="form-group">
        <label for="user-name">Nome</label>
        <input 
          type="text" 
          id="user-name" 
          placeholder="Digite seu nome" 
          @input="updateUserName"
          :value="userInfo.name"
        >
      </div>

      <div class="form-group">
        <label for="user-surname">Sobrenome</label>
        <input 
          type="text" 
          id="user-surname" 
          placeholder="Digite seu sobrenome" 
          @input="updateUserSurname"
          :value="userInfo.surname"
        >
      </div>
    </form>
  </div>
</template>

<script>
  export default {
    props: {
      userInfo: Object
    },
    data() {
      return {
        imageSrc: ""
      };
    },
    methods: {
      updateUserName(event) {
        this.$emit('update-user-name', event.target.value.trim());
      },
      updateUserSurname(event) {
        this.$emit('update-user-surname', event.target.value.trim());
      },
      openFileUpload() {
        this.$refs.fileInput.click();
      },
      handleImageUpload(event) {
        const file = event.target.files[0];
        if (file) {
          const reader = new FileReader();
          reader.onload = () => {
            this.imageSrc = reader.result;
            this.$emit('image-loaded', reader.result);
          };
          reader.readAsDataURL(file);
        }
      }
    },
    created() {
      this.$emit('update-user-name', 'ADMINISTRADOR');
      this.$emit('update-user-surname', 'IMÓVELGUIDE');
    },
  }
</script>

<style scoped>
  .user-panel-container {
    display: grid;
    box-sizing: border-box;
    border: .25rem solid var(--gray);
    padding: 1.25rem 1.5rem;
  }

  .user-profile-container {
    justify-self: center;
    width: 116px;
  }

  .user-profile-container__img {
    display: block;
    box-sizing: border-box;
    border: .125rem solid var(--dark-grey);
    height: 120px;
    margin-bottom: .5rem;
  }

  .user-profile-container__img img {
    object-fit: cover;
    width: 100%;
    height: 100%;
  }

  .add-photo-btn {
    background-color: var(--orange);
    border: none;
    cursor: pointer;
    color: var(--white);
    text-transform: uppercase;
    font-size: .75rem;
    padding: .375rem;
    margin-bottom: 1rem;
    transition: all .3s ease-in-out;
  }

  .add-photo-btn:hover {
    background: var(--yellow);
  }

  .user-form-container {
    justify-self: center;
    display: flex;
    flex-direction: column;
    gap: .875rem;
  }

  .form-group label {
    font-size: .75rem;
    margin-bottom: .25rem;
    display: block;
  }

  .form-group input {
    outline: none;
    border: .125rem solid var(--gray);
    padding: .5rem .375rem;
    font-size: .75rem;
    text-transform: uppercase;
    transition: all .3s ease-in-out;
  }

  .form-group input:focus {
    border-color: var(--yellow);
  }

  @media (min-width: 768px) {
    .user-panel-container {
      grid-template-columns: auto 1fr;
      column-gap: .875rem;
    }

    .add-photo-btn {
      margin: 0;
    }
  }
</style>