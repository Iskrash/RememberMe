<template>
  <div>
    <base-dialog v-if="inputIsValid" title="Warning: Invalid input" @close="closeDialog"> <!-- close event - is emit,
                                                                                           closeDialog will be launched after click  -->
      <template #default>
        <p>At least one input value is invalid</p>
        <p>Make sure you enter at least a few characters into each input field.</p>
      </template>
      <template #actions>
        <base-button mode="center" @click="closeDialog">Confirm</base-button>
      </template>
    </base-dialog>
  </div>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Text</label>
        <input id="title" name="title" type="text" ref="titleInput">
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea id="description" name="description" rows="3" ref="descInput"></textarea>
      </div>
      <div class="form-control">
        <label for="title">Link</label>
        <input id="link" name="link" type="url" ref="linkInput">
      </div>
      <div class="custom">
        <base-button type="submit" mode="right">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  data() {
    return {
      inputIsValid: false,
    }
  },
  inject: ['addResource'],
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value
      const enteredDesc = this.$refs.descInput.value
      const enteredLink = this.$refs.linkInput.value

      if (enteredTitle.trim() === '' || enteredDesc.trim() === '' || enteredLink.trim() === '') {
        this.inputIsValid = true
      } else {
        this.addResource(enteredTitle, enteredDesc, enteredLink)
        this.clearData()
      }
    },
    closeDialog() {
      this.inputIsValid = false
    },
    clearData() {
      this.$refs.linkInput.value = ''
      this.$refs.descInput.value = ''
      this.$refs.titleInput.value = ''
    }
  }
}
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>