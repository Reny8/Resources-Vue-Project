<template>
  <section v-if="showForm">
    <form @submit.prevent="addItem(newResource)">
      <label> Title</label>
      <input placeholder="Enter a title..." v-model="newResource.title" />

      <label> Description</label>
      <textarea
        placeholder="Enter a description here..."
        v-model="newResource.description"
      ></textarea>

      <label> Link</label>
      <input
        placeholder="Provide a link..."
        v-model="newResource.link"
        type="url"
      />

      <button>add resource</button>
    </form>
  </section>
  <teleport to="#app">
    <AlertBox :open="open" :toggleAlertBox="toggleAlertBox"
  /></teleport>
</template>
<script>
import AlertBox from './AlertBox.vue';
export default {
  name: 'AddResource',
  components: {
    AlertBox,
  },
  props: ['handleAdd', 'showForm'],
  data() {
    return {
      open: false,
      newResource: {
        title: '',
        description: '',
        link: '',
      },
    };
  },
  methods: {
    addItem(item) {
      if (item.title === '' || item.description === '' || item.link === '') {
        this.toggleAlertBox();
        return;
      }
      this.handleAdd(item);
      this.newResource = {
        title: '',
        description: '',
        link: '',
      };
    },
    toggleAlertBox() {
      this.open = !this.open;
    },
  },
};
</script>
<style scoped>
form {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 0.3rem;
  padding: 1rem;
}
label {
  font-weight: 700;
}
textarea,
input {
  width: 99.1%;
  border: solid 1px #7d7d7d;
  border-radius: 3px;
  height: 2rem;
  padding-left: 7px;
}
button {
  width: 100%;
  text-transform: uppercase;
  margin-top: 1rem;
  background-color: #360b59;
  box-shadow: rgba(0, 0, 0, 0.2) 0px 2px 7px -1px,
    rgba(0, 0, 0, 0.14) 0px 1px 1px 0px, rgba(0, 0, 0, 0.12) 0px 1px 3px 0px;
  color: white;
  border: none;
  padding: 1rem;
  border-radius: 3px;
  font-weight: 700;
}
button:hover {
  background-color: #360b5988;
  cursor: pointer;
}
textarea {
  resize: none;
  height: 4rem;
  font-family: Arial, Helvetica, sans-serif;
  padding-top: 10px;
}
</style>
