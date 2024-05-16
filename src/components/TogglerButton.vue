<!-- TogglerButton.vue -->
<template>
    <button @click="clicked"> {{ button_text }}</button>
  </template>
  
  <script>
  export default {
    name: "TogglerButton",
    props:["component"],
    data() {
      return {
        button_state: 0,
        button_text: "off"
      };
    },
    methods: {
      toggler() {
        this.button_state = this.button_state === 1 ? 0 : 1;
        if (this.button_state === 0) {
          this.button_text = "off";
        } else if (this.button_state === 1) {
          this.button_text = "on";
          
        }
      },
      clicked() {
        this.toggler();
        const component = { component: this.component, state: this.button_state };
        console.log(component);
          this.$emit('button-on-click', component);
      }
    }
  };
  </script>
  