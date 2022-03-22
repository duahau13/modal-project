<template>
  <div v-if="currentRecord">
    <h1>{{ title }}</h1>
    <p>Hello {{ currentRecord.Name }}</p>
  </div>
  <div v-else><p>Loading</p></div>
  <div v-if="showModal">
    <Modal theme="" @close="toggleModal">
      <h1>Sign up for entrance</h1>
      <p>Grab your copy at half price!</p>
      <template v-slot:links>
        <a href="#">sign up now</a>
        <a href="#">more info</a>
      </template>
    </Modal>
  </div>
  <div v-if="showModalTwo">
    <Modal @close="toggleModalTwo">
      <h1>Get the newsletter</h1>
      <p>Latest promotion and codes.</p>
    </Modal>
  </div>
  <button @click="toggleModal">Toggle modal</button>
  <button @click="toggleModalTwo">Toggle modal</button>
</template>

<script>
import Modal from "./components/Modal.vue";

export default {
  name: "App",
  data() {
    return {
      title: "My First Vue App",
      showModal: false,
      showModalTwo: false,
      currentRecord: null,
    };
  },
  components: {
    Modal,
  },
  methods: {
    toggleModal() {
      this.showModal = !this.showModal;
    },
    toggleModalTwo() {
      this.showModalTwo = !this.showModalTwo;
    },
  },
  mounted() {
    grist.ready();
    grist.onRecord((record) => (this.currentRecord = record));
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
