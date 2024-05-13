<template>
    <div :class="['buttonCalc', { 'operator': isOperator }]" @click="handleClick">
      {{ buttonText }}
    </div>
  </template>
  
  <script>
  export default {
    props: {
      buttonText: {
        type: [String, Number],
        required: true
      },
      isOperator: {
        type: Boolean,
        default: false
      }
    },
    methods: {
      handleClick() {
        this.$emit('button-click', this.buttonText);
      }
    }
  }
  </script>
  
  <style scoped>
  .buttonCalc {
      flex: 0 0 calc(25% - 0.5rem);
      padding: 1rem;
      text-align: center;
      font-size: 1.25rem;
      font-weight: bold;
      color: #fff;
      border-radius: 0.25rem;
      background-color: #31475e;
  }
  
  .buttonCalc.operator {
      background-color: #3f76b9;
  }
  
  .buttonCalc:hover {
      cursor: pointer;
      background-color: #3d4975;
  }
  </style>