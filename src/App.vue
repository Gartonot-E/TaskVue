<template>
  <div>
    <MyHeader @sortName="sortName"/>
    <MyMain :products="products"/>
  </div>
</template>
<script>
  import MyHeader from '@/components/MyHeader'
  import MyMain from '@/components/MyMain'

  export default {
    components: { MyHeader, MyMain },
    data() {
      return {
        products: [
          { id: 1, imgUrl: 'https://placekitten.com/330/200', title: 'Кот Борис', body: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', price: '10 000' },
          { id: 2, imgUrl: 'https://placekitten.com/330/200', title: 'Албанская порода', body: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', price: '15 000' }
        ]
      }
    },
    methods: {
      sortName(data) {
        if (data == 'max') {
          this.products.sort( (a, b) => {
            a = +a.price.replace(' ', '');
            b = +b.price.replace(' ', '');
            return b - a;
          });
        }
        if (data == 'min') {
          this.products.sort( (a, b) => {
            a = +a.price.replace(' ', '');
            b = +b.price.replace(' ', '');
            return a - b;
          });
        }

        if (data == 'title') {
          this.products.sort( (a, b) => {
              if (a.title > b.title) { return 1; }
              if (a.title < b.title) { return -1; }
              return 0;
          });
        }
        
      }
    }
  }
</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Inter:wght@600&family=Source+Sans+Pro:wght@400;600&display=swap');

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    background: rgba(255, 254, 251, 0.8);
    color: #3F3F3F;
    font-family: "Source Sans Pro";
}

.container {
    width: 87.15%;
    margin: 0 auto;
}

</style>
