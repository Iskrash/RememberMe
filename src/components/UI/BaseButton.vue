<template>
  <button :class="mode">
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: ['mode'],
  data() {
    return {

    }
  },

}
</script>

<style scoped>
button {
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  background-color: #640032;
  border: 1px solid #3a0061;
  color: white;
  cursor: pointer;
}

button:hover,
button:active {
  background-color: #783da0;
  border-color: #270041;
}

.flat {
  background-color: transparent;
  color: #3a0061;
  border: none;
}

.flat:hover,
.flat:active {
  background-color: #edd2ff;
}

.center {
  /* margin: auto; / use auto-margin if u want to center button, but "width: 100%" must be deleted */
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%; /* the button take all place */
}

.right {
  margin-left: auto; /* without margin will no working */
  display: flex;
  align-items: center;
  justify-content: flex-end;
}
</style>