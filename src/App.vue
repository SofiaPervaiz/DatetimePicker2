<template>
  <div id="app">
    <button class="scheduler-open" v-on:click="toggleModal">
      Questions? Schedule a Call &#9742;
    </button>
    <SchedulerModal
      v-bind:showModal="showModal"
      v-bind:toggleModal="toggleModal"
    />
  </div>
</template>

<script>
import SchedulerModal from "./components/SchedulerModalComponent.vue";

export default {
  name: "App",
  components: {
    SchedulerModal,
  },
  methods: {
    toggleModal: function () {
      this.showModal = this.showModal ? false : true;
    },
  },
  data() {
    return {
      showModal: false,
    };
  },
};
</script>
