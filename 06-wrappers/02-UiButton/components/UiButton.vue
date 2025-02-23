<template>
  <component :is="tag" class="button" :class="buttonClassList" :type="buttonType">
    <slot />
  </component>
</template>

<script>

const classDefinitions = {
  primary: 'button_primary',
  secondary: 'button_secondary',
  danger: 'button_danger',
  block: 'button_block',
};

export default {
  name: 'UiButton',

  props: {
    
    tag: {
      type: [String, Object],
      default: 'button',
    },

    variant: {
      type: String,
      default: 'secondary',
    },

    block: {
      type: Boolean,
      default: false
    },

  },

  computed: {
    
    buttonClassList() {
      const res = [];
      res.push(classDefinitions[this.variant])
      if(this.block) {
        res.push(classDefinitions['block']);
      }
      return res;
    },

    buttonType() {
      if (typeof this.tag === 'string' && this.tag.toLowerCase() === 'button') {
        return this.$attrs.type || 'button';
      }
      return this.$attrs.type;
    },

  },
};
</script>

<style scoped>
.button {
  display: inline-block;
  padding: 10px 24px;
  font-weight: 700;
  font-size: 20px;
  line-height: 28px;
  color: initial;
  text-align: center;
  border: 4px solid transparent;
  transition-duration: 0.2s;
  transition-property: background-color, border-color, color;
  outline: none;
  box-shadow: none;
  background-color: transparent;
  cursor: pointer;
  text-decoration: none;
}

.button.button_block {
  display: block;
  width: 100%;
}

.button_primary {
  background-color: var(--blue);
  border-color: var(--blue);
  color: var(--white);
}

.button_primary:hover {
  background-color: var(--blue-light);
  border-color: var(--blue-light);
}

.button_secondary {
  background-color: var(--white);
  border-color: var(--blue);
  color: var(--blue);
}

.button_secondary:hover {
  border-color: var(--blue-light);
}

.button_danger {
  background-color: var(--white);
  border-color: var(--red);
  color: var(--red);
}

.button_danger:hover {
  border-color: var(--red-light);
}
</style>
