<template>
  <section class="product">
    <h1 class="title">{{ title }}</h1>
    <div class="container">
      <div class="product__wrap">
        <Product 
          v-for="(product, i) of dataProduct" 
          :key="product.title + i"
          :product="product"
          @changeselected="changeSelected($event)"
          @leavechange="leaveChange($event)"
          @enterchange="enterChange($event)"
        />
      </div>
    </div>
  </section>
</template>
<script>
import Product from "./components/Product";
export default {
  components: {
    Product
  },
  data() {
    return {
      time: null,
      title: 'Ты сегодня покормил кота?',
      dataProduct: [
        {
          id: 0,
          title: 'Нямшука',
          supTitle: 'Сказачное заморское яство',
          volume: '0,5',
          status: null,
          list: ['10 порций', 'мышь в подарок'],
          text: 'Печень утки разварная с артишоками.',
          flavor: 'с фуа-гра',
          hover: false
        },
        {
          id: 1,
          title: 'Нямшука',
          supTitle: 'Сказачное заморское яство',
          volume: '2',
          status: null,
          list: ['40 порций', '2 мыши в подарок'],
          text: 'Головы щучьи с чесноком да свежайшая сёмгушка.',
          flavor: 'с рыбой',
          hover: false
        },
        {
          id: 2,
          title: 'Нямшука',
          supTitle: 'Сказачное заморское яство',
          volume: '5',
          status: 'disabled',
          list: ['100 порций', '5 мышей в подарок', 'заказчик доволен'],
          text: 'Филе из циплят в трюфеле в бульоне.',
          flavor: 'с курой',
          hover: false
        }
      ]
    }
  },
  methods: {
    changeSelected(e) {
      this.dataProduct[e].hover = false
      if(this.dataProduct[e].status === 'disabled') {
        return;
      } else if(this.dataProduct[e].status === 'selected') {
        this.dataProduct[e].status = null;
        console.log(1);
      } else {
        this.dataProduct[e].status = 'selected';
      }
    },
    leaveChange(e) {
      if(this.dataProduct[e].status === 'disabled') return;
      clearTimeout(this.time);
      this.time = setTimeout(() => {
        this.dataProduct[e].hover = true;
      }, 1000)
    },
    enterChange(e) {
      clearTimeout(this.time)
      this.dataProduct[e].hover = false;
    }
  }
}
</script>