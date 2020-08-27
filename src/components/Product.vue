<template>
  <div 
    class="product__item"
    :class="{'selected': product.status === 'selected', 'hovered' : product.hover, 'disabled': product.status === 'disabled'}"
  >
    <div class="product__card" @click="selectedChange" @mouseleave="leaveChange" @mouseenter="enterChange">
      <div class="overlay"></div>
      <span class="product__suptitle" >{{ product.title }}</span>
      <span class="product__suptitle hovered__text">Котэ не одобряет?</span>
      <span class="product__title">Нямушка</span>
      <span class="product__subtitle">{{ product.flavor }}</span>
      <ul class="product__list" >
        <li
          v-for="listItem of product.list" 
          :key="listItem"
        >{{ listItem }}</li>
      </ul>
      <div class="product__volume">
        <span class="product__volume-num">{{ product.volume }}</span>
        <span class="product__volume-text">кг</span>
      </div>
    </div>
    <p class="product__buy" v-if="product.status === 'selected'">
      {{ product.text }}
    </p>
    <p class="product__buy" v-else-if="product.status === 'disabled'" style="color: #d1d152">
      Печалька, {{ product.flavor }} закончился.
    </p>
    <p class="product__buy" v-else>
      Чего сидишь? Порадуй котэ, <span class="product__buy-link" @click="selectedChange">купи.</span>
    </p>
  </div>
</template>
<script>
export default {
  props: ['product'],
  methods: {
    selectedChange() {
      this.$emit('changeselected', this.product.id);
    },
    leaveChange() {
      this.$emit('leavechange', this.product.id)
    },
    enterChange() {
      this.$emit('enterchange', this.product.id)
    }
  }
}
</script>