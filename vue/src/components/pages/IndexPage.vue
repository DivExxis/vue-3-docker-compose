<template>
  Index

  <div>
    <RouterLink :to="{ name: $routes.EXAMPLE }">
     To Example
    </RouterLink>
  </div>
  <div>
    <RouterLink :to="{ name: $routes.PROM }">
      To PROM
    </RouterLink>
  </div>


  <div class="grid">
    <div class="grid__item">
      123
    </div>
    <div class="grid__item">
      123
    </div>

    <Btn :pr="1" @click="() => myClick()" @more="(v) => more(v)">Нажать</Btn>
    <Btn v-if="p > 30" :pr="2">Ого!!!</Btn>
    <Btn v-else :pr="2">NONONO</Btn>

    <Btn v-for="i in r">FOR {{ i }}</Btn>

    <input v-model="text" />

    <input :value="text" @input="(e) => setText(e.target.value)" />

    {{ ppo }}

    <template v-if="p > 0">
      <Btn :pr="5"/>
      <Btn :pr="p"/>
    </template>
  </div>
</template>

<script lang="ts">
import Btn from './../ui/Btn.vue'
import {mapGetters, mapActions} from "vuex";

export default {
  name: 'IndexPage',
  components : {
    Btn
  },
  data () {
    return {
      p: 1,
      r: [1, 2, 5],
      text: ''
    }
  },
  computed: {
    ...mapGetters({
      ppo: 'getCount'
    }),
  },
  methods: {
    ...mapActions([
      'runIncrement'
    ]),
    myClick() {
      this.p += 10
    },
    more (v) {
      this.runIncrement(1)
    },
    setText (v) {
      this.text = v
    }
  }
}
</script>

<style scoped lang="scss">
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;

  &__item {
    border: 1px solid red;
    color: green;

    &--full {
      color: red;
    }
  }
}

</style>
