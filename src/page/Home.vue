<template>
  <main class="main">
    <UserPanel       
      @update-user-name="updateUserName" 
      @update-user-surname="updateUserSurname" 
      @image-loaded="updateUserImage"
      :userInfo="userInfo"
    />
    <UserCard :name="userInfo.name" :surname="userInfo.surname" :image="userImage" />
  </main>
</template>

<script>
  import UserPanel from "../components/UserPanel.vue";
  import UserCard from "../components/UserCard.vue";

  export default {
    components: { 
      UserPanel,
      UserCard
    },
    data() {
      return {
        userInfo: {
          name: 'Administrador',
          surname: 'ImóvelGuide'
        },
        userImage: "",
      };
    },
    methods: {
      updateUserName(name) {
        this.userInfo.name = name;
      },
      updateUserSurname(surname) {
        this.userInfo.surname = surname;
      },
      updateUserImage(image) {
        this.userImage = image;
      },
    }
  }
</script>

<style scoped>
  .main {
    display: grid;
    row-gap: 3.5rem;
  }
</style>