<template>
  <div id="app">
      <h1 v-text="title"></h1>
      <input type="text" v-model="newItem" v-on:keyup.enter="addNew" placeholder="add project">
      <ul>
          <li v-for="item in items" v-bind:class="{finshed:item.isFinished}" v-on:click="toggleFinshed(item)">
              {{item.label}}
          </li>
      </ul>
      <!-- 父组件给子组件传参数 -->
      <component-a msgfromparent='来自爸爸的问候' v-on:child-tell-me-sth="listenToChild"></component-a>

      <!-- 子组件给父组件传参数 -->
      <h1>儿子传过来的：{{childTellMeMsg}}</h1>
  </div>
</template>

<script>
    import Store from './store.js';
    import ComponentA from './components/ComponentA.vue';
    console.log(Store);
    export default {
      data: function() {
          return {
                    title: 'This is a toodlist',
                    items: Store.fetch(),
                    newItem: '',
                    childTellMeMsg: ''
              }
          },
          components: {
              ComponentA
          },
          watch: {
              //当items变化时候，执行
              items: {
                  handler: function(items) {
                      Store.save(items);
                  },
                  deep: true
              }
          },
          methods: {
              toggleFinshed: function(item) {
                  item.isFinished = !item.isFinished;
              },
              addNew: function() {
                  if(this.newItem) {
                      this.items.push({
                          label: this.newItem,
                          isFinished: false
                      });
                      this.newItem = '';
                  }
              },
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
