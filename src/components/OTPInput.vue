<template>
  <div class="flex flex-row justify-between">
    <input
      :style="style"
      v-model="inputs[idx]"
      :class="inputClass"
      @keyup="inputFocus"
      @focus="check($event)"
      @change="handleChange(idx, $event)"
      v-for="(inp, idx) in inputCount"
      :key="idx"
      :tabindex="idx"
      maxlength="1"
      autocomplete="off"
    />
  </div>
</template>
<script>
export default {
  props: {
    inputCount: {
      type: Number,
      default: 4,
    },
    inputClass: String,
    dimension: {
      type: String,
      default: "30px",
    },
    value: [String, Number, Object],
  },
  computed: {
    style() {
      return `
        width: ${this.dimension}; 
        height: ${this.dimension}; 
        text-align: center;
      `;
    },
  },
  data() {
    return {
      inputs: Array(this.inputCount),
      currentKey: 0,
    };
  },
  watch: {
    value() {
      this.inputs = this.value.split("");
    },
  },
  methods: {
    handleChange(key, event) {
      this.inputs[key] = event.target.value;
    },

    getChildren(event) {
      return event.target.parentElement.children;
    },

    check(event) {
      const inputs = this.getChildren(event);

      if (inputs[this.currentKey]){
        inputs[this.currentKey].focus();
      }
    },

    inputFocus(event) {
      const data = this.inputs.join("");
      const inputs = this.getChildren(event);

      this.$emit("input", data);
      if (data.length === this.inputCount) {
        this.$emit("completed", data);
      }

      if (event.key === "Delete" || event.key === "Backspace") {
        this.currentKey--;
        if (this.currentKey <= 0) {
          this.currentKey = 0;
        }
        if (inputs[this.currentKey]) {
          inputs[this.currentKey].focus();
        }
      } else {
        this.currentKey++;
        if (this.currentKey >= this.inputCount) {
          this.currentKey = this.inputCount;
        }
        if (inputs[this.currentKey]) {
          inputs[this.currentKey].focus();
        }
      }
    },
  },
}
</script>
<style>
  /* Otp css here */
</style>
