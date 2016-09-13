<template>
  <div id="app">
      <h1 v-text="title"></h1>
      <!-- 父组件给子组件传参数 -->
      <component-a msgfromparent='来自爸爸的问候' v-on:child-tell-me-sth="listenToChild"></component-a>

      <!-- 子组件给父组件传参数 -->
      <h1>儿子传过来的：{{childTellMeMsg}}</h1>
  </div>
</template>

<script>
    import ComponentA from './components/ComponentA.vue';

    export default {
      data: function() {
          return {
                    childTellMeMsg: ''
              }
          },
          components: {
              ComponentA
          },

          methods: {
              listenToChild: function(msg) {
                //   msg子组件传过来的参数
                  this.childTellMeMsg = msg
              }
          }
    }
</script>
<style>
    html {
      height: 100%;
    }

    body {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100%;
    }

    #app {
      color: #2c3e50;
      margin-top: -100px;
      max-width: 600px;
      font-family: Source Sans Pro, Helvetica, sans-serif;
      text-align: center;
    }

    #app a {
      color: #42b983;
      text-decoration: none;
    }
    .finshed {
        text-decoration: line-through;
    }
    .logo {
      width: 100px;
      height: 100px
    }
</style>
