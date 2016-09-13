<template>
    <h1>This is component a</h1>
    <input type="button" name="name" value="ClickMe" v-on:click='onClickMe' />
    <h2>这里也能读到父组件传过来的值：{{msgfromparent}}</h2>
</template>

<script>
export default {
  data() {
    return {
        msg: '爸爸您辛苦了'
    };
  },
  props: ['msgfromparent'],
  methods: {
      onClickMe: function() {
          //父组建传过来的参数
          console.log(this.msgfromparent);
          //触发父组件绑定的方法
          this.$emit('child-tell-me-sth', this.msg);
      }
  }
};
</script>

<style lang="css">
</style>
