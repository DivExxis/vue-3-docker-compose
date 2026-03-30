<template>
  <button class="btn" @click="() => add()">
    <slot>
      Кнопка
    </slot>
    <span>{{ count }}, {{ r3 }}</span>
  </button>
</template>


<script>
import {computed} from "vue";

export default {
  name: 'Btn',
  props: {
    pr: {
      type: Number,
      default: 0,
      // required: true
    }
  },
  emits: ['more'],
  data () {
    return {
      count: 0
    }
  },
  provide: {
    c: computed(() => this.count)
  },
  computed: {
    r2 () {
      return this.count * this.count
    },
    r3 () {
      return this.r2 * this.count * this.pr
    }
  },
  methods: {
    add () {
      this.count += 1

      if (this.count > 10) {
        this.$emit('more', this.count)
      }
    }
  }
}
</script>


<style scoped lang="scss">
.btn{
  border: none;
  background: #00d389;
  color: black;
  font-size: 18px;
  padding: 10px 20px;
}
</style>