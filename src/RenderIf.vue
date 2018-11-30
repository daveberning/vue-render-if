<template>
  <component :is="tag" v-if="ableToRender">
    <slot />
  </component>
</template>

<script>
export default {
  props: {
    defined: { required: true },
    tag: { type: String, required: false, default: 'div', },
    notValid: { required: false }
  },
  methods: {
    convertStringToArray(prop) {
      return (!Array.isArray(prop)) ? prop = [prop] : prop
    },
  },
  computed: {
    ableToRender() {
      let rendered = true;
      let defined = this.convertStringToArray(this.defined);
      let notValid = this.convertStringToArray(this.notValid);

      console.log(defined);
      console.log(notValid);

      defined.forEach(item => {
        if (this.notValid === undefined) {
          if (item === null || item === undefined || item === '') rendered = false;
        } else {
          notValid.forEach((n) => {
           if (item === n) rendered = false;
          });
        }
      });
      return rendered;
    }
  }
};
</script>