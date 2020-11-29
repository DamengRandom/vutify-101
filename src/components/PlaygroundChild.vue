<template>
  <div>
    <input :value="textFromParent" @input="changeText" />
    <p>child view: {{ childText }}</p>
  </div>
</template>

<script>
export default {
  name: "PlaygroundChild",
  props: ["textFromParent"],
  data() {
    return {
      childText: ""
    };
  },
  methods: {
    changeText(event) {
      this.childText = event.target.value;
      this.$emit("updateTextContent", this.childText);
    }
  }
};
</script>
<style scoped></style>
