<template>
  <div id="app">
    
    <h1 class="title">My BTC Wallet</h1>  

    <div class="columns">
      <div class="column">
        Account

        <div class="field has-addons">
          <p class="control">
            <input v-model="address" class="input" type="text" placeholder="Your address">
          </p>
          <p class="control">
            <a class="button is-static">
              {{ balance }} BTC
            </a>
          </p>
          <p class="control">
            <input v-model="privateKey" class="input" type="text" placeholder="Your private key">
          </p>
        </div>

        Send to:
        <div class="field">
          <p class="control has-icons-left has-icons-right">
            <input v-model="addressTo" class="input" type="text" placeholder="Address">
            <span class="icon is-small is-left">
              <i class="fa fa-envelope"></i>
            </span>
            <span class="icon is-small is-right">
              <i class="fa fa-check"></i>
            </span>
          </p>
        </div>
        <div class="field">
          <p class="control has-icons-left">
            <input v-model="amountTo" class="input" type="text" placeholder="Amount">
            <span class="icon is-small is-left">
              <i class="fa fa-lock"></i>
            </span>
          </p>
        </div>
        <div class="field">
          <p class="control">
            <button class="button is-success" @click="send">
              Send
            </button>
          </p>
        </div>

      </div>
      <div class="column">
        Transactions:

        <article v-for="(value, key, index) in transactions" class="message is-primary">
          <div class="message-header">
            <p>Header</p>
          </div>
          <div class="message-body">
            Description
          </div>
        </article>

      </div>
  </div>

  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      address: '',
      privateKey: '',
      balance: 0,
      addressTo: '',
      amountTo: '',
      transactions: []
    }
  },
  watch: {
    address (val, oldVal) {
      this.balance = 0
    }
  },
  methods: {
    send () {
      alert(`Send ${this.amountTo}`)
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin:50px;
}

.columns{
  text-align: left;
}
</style>
