<!-- src/components/layout/The LoginModal TEST -->
<template>
  <div>
    <BaseModal>
      <transition name="fade" mode="out-in">
        <component v-bind:is="currentFormComponent"></component>
      </transition>
    </BaseModal>
  </div>
</template>
<script>
import BaseModal from "../../components/event/BaseModal.vue";
import TheLoginForm from "./TheLoginForm.vue";
import TheRegisterForm from "./TheRegisterForm.vue";
import bus from "../../bus";

export default {
  name: "TheLoginRegisterModal",
  components: { BaseModal, TheLoginForm, TheRegisterForm },
  props: {},
  created() {
    bus.$on("form-switch", this.switchForm);
  },
  destroyed() {
    bus.$off("form-switch", this.switchForm);
  },
  data() {
    return {
      currentForm: "",
    };
  },
  computed: {
    currentFormComponent() {
      if (this.currentForm === "") return;
      return `The${this.currentForm}Form`;
    },
  },
  methods: {
    switchForm(form) {
      this.currentForm = form;
    },
  },
};
</script>
<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s !important;
}
.fade-enter,
.fade-leave-to {
  opacity: 0 !important;
}
</style>
