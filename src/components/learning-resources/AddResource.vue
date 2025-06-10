<template>
  <base-dialog
    v-if="inputIsInvalid"
    title="Invalid Input"
    @close="confirmError"
  >
    <p>Unfortunately, at least one input value is invalid.</p>
    <p>
      Please check all inputs and make sure you add a few characters into the
      fields.
    </p>

    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>

  <!-- Accessibility Toggle Card -->
  <base-card class="accessibility-card">
    <div class="toggle-container">
      <p class="toggle-label">Accessibility Helper Descriptions</p>
      <base-button
        @click="toggleA11yHelp"
        :class="{ active: showA11yHelp }"
      >
        {{ showA11yHelp ? 'Hide Descriptions' : 'Show Descriptions' }}
      </base-button>
    </div>
  </base-card>

  <!-- Main Form Card -->
  <base-card>
    <form @submit.prevent="submitData">
      <!-- Title Field -->
      <div class="form-control">
        <label for="title">Enter the resource title</label>
        <input
          id="title"
          name="title"
          type="text"
          ref="titleInput"
          :aria-describedby="showA11yHelp ? 'title-desc' : null"
        />
        <p
          v-if="showA11yHelp"
          id="title-desc"
          :class="['sr-only', { visible: showA11yHelp }]"
        >
          This will be the name shown for the resource.
        </p>
      </div>

      <div class="form-control">
        <label for="description">Enter a short description</label>
        <textarea
          id="description"
          name="description"
          rows="3"
          ref="descInput"
          :aria-describedby="showA11yHelp ? 'description-desc' : null"
        ></textarea>
        <p
          v-if="showA11yHelp"
          id="description-desc"
          :class="['sr-only', { visible: showA11yHelp }]"
        >
          Briefly explain what this resource covers.
        </p>
      </div>

      <div class="form-control">
        <label for="link">Enter the resource link</label>
        <input
          id="link"
          name="link"
          type="url"
          ref="linkInput"
          :aria-describedby="showA11yHelp ? 'link-desc' : null"
        />
        <p
          v-if="showA11yHelp"
          id="link-desc"
          :class="['sr-only', { visible: showA11yHelp }]"
        >
          Provide a valid URL starting with https://
        </p>
      </div>

<div class="submit-button-container">
  <base-button type="submit">Add Resource</base-button>
</div>

    </form>
  </base-card>
</template>

<script>
export default {
  inject: ['addResource'],
  data() {
    return {
      inputIsInvalid: false,
      showA11yHelp: false,
    };
  },
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descInput.value;
      const enteredUrl = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredUrl.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }

      this.addResource(enteredTitle, enteredDescription, enteredUrl);
    },
    confirmError() {
      this.inputIsInvalid = false;
    },
    toggleA11yHelp() {
      this.showA11yHelp = !this.showA11yHelp;
    },
  },
};
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

#title,
#link {
  padding: 0.5rem;
  height: 2.5rem;
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

.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}

.sr-only.visible {
  position: static;
  width: auto;
  height: auto;
  margin-top: 0.25rem;
  clip: auto;
  white-space: normal;
  color: #555;
  font-size: 0.875rem;
}

.accessibility-card {
  margin-bottom: 1.5rem;
  padding: 1rem;
}

.toggle-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.toggle-label {
  font-size: 1rem;
  font-weight: 600;
  margin: 0;
}

.base-button.active {
  background-color: #3a0061;
  color: white;
}

.submit-button-container {
  display: flex;
  justify-content: flex-end;
  margin-top: 1.5rem;
}

</style>
