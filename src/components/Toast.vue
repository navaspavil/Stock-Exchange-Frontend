<template>
  <div
    v-if="visible"
    class="fixed top-5 right-5 border p-4 rounded-lg shadow-lg"
    :class="{
      'bg-red-50 text-red-600 border-red-600': isError,
      'bg-green-50 text-green-600 border-green-600': !isError,
    }"
  >
    {{ message }}
  </div>
</template>

<script>
export default {
  name: "ToastComponent",
  data() {
    return {
      visible: false,
      message: "",
      isError: false,
    };
  },
  methods: {
    show(msg, error = false) {
      this.message = msg;
      this.isError = error;
      this.visible = true;
      setTimeout(() => {
        this.visible = false;
      }, 3000);
    },
  },
};
</script>
