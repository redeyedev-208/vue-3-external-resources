<template>
  <teleport to="body">
  <div @click="$emit('close')"></div>
  <dialog open ref="dialogElement" tabindex="-1" role="dialog" aria-modal="true"
    :aria-labelledby="title ? 'dialog-title' : null" aria-describedby="dialog-description">
    <header>
      <slot name="header">
        <h2 id="dialog-title">{{ title }}</h2>
      </slot>
    </header>
    <section id="dialog-description">
      <slot></slot> <!-- default slot with message text -->
    </section>
    <menu>
      <slot name="actions">
        <base-button @click="$emit('close')">Close</base-button>
      </slot>
    </menu>
  </dialog>
  </teleport>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: false,
    },
  },
  emits: ['close'],
  mounted() {
    this.$refs.dialogElement?.focus();
    document.addEventListener('keydown', this.handleEscape);
  },
  beforeUnmount() {
    document.removeEventListener('keydown', this.handleEscape);
  },
  methods: {
    handleEscape(event) {
      if (event.key === 'Escape') {
        this.$emit('close');
      }
    }
  }
}
</script>

<style scoped>
div {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.75);
  z-index: 10;
}

dialog {
  position: fixed;
  top: 20vh;
  left: 10%;
  width: 80%;
  z-index: 100;
  border-radius: 12px;
  border: none;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 0;
  margin: 0;
  overflow: hidden;
}

header {
  background-color: #3a0061;
  color: white;
  width: 100%;
  padding: 1rem;
}

header h2 {
  margin: 0;
}

section {
  padding: 1rem;
}

menu {
  padding: 1rem;
  display: flex;
  justify-content: flex-end;
  margin: 0;
}

@media (min-width: 768px) {
  dialog {
    left: calc(50% - 20rem);
    width: 40rem;
  }
}
</style>
