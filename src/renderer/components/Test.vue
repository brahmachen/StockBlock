<template>
    <div>
        <h1 style="margin: 0">
            {{price.split('.')[0]}}.
            <small>{{price.split('.')[1]}}</small>
        </h1>
    </div>
</template>

<script>
export default {
  data () {
    return {
      price: ""
    }
  },
  mounted () {
    let timer = () => {
        setTimeout(async () => {
            this.price = await this.getPrice();
            timer();
        },1000);
    }
    timer();
  },
  methods: {
    getPrice(){
        return new Promise((resolve, reject) => {
            this.$http.get("http://hq.sinajs.cn/list=sh603000")
            .then(res => {
                let resArr = res.data.split(',');
                resolve(resArr[3]);
            })
        })
    }
  }
}
</script>
<style>
</style>