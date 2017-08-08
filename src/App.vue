<template>
  <div id="app">
    
    <h1 class="title">My BTC Wallet</h1>  

    <div class="columns">
      <div class="column">
        Account

        <div class="field has-addons">
          <p class="control">
            <input v-model="addressWIF" class="input" type="text" placeholder="Your address WIF (Private key)">
          </p>
          <p class="control">
            <a class="button is-static">
              {{ balance }} BTC
            </a>
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

        <div class="field has-addons">
          <div class="control">
            <a class="button is-info" @click="generateNewAddress">
              Generate new address
            </a>
          </div>
          <div class="control">
            <input v-model="newAddress" class="input" type="text" placeholder="New address will appear here">
          </div>
        </div>

      </div>
      <div class="column">
        Transactions (Total: {{ transactions.totalNum }}): 
        <p class="field">
          <a class="button" @click="refreshTransactions">
            Refresh
          </a>
        </p>

        <article v-for="(item, key, index) in transactions.items" class="message is-primary transaction">
          <div class="message-header">
            <p>{{ item.txid }}</p>
          </div>
          <div class="message-body">
            <tree-view :data="item" :options="{maxDepth: 0}"></tree-view>
          </div>
        </article>

      </div>
  </div>

  </div>
</template>

<script>
import axios from 'axios'
import bitcoin from 'bitcoinjs-lib'

window.bitcoin = bitcoin
var apiUrl = 'https://test-insight.bitpay.com/api'

export default {
  name: 'app',
  data () {
    return {
      addressWIF: '',
      address: '',
      privateKey: '',
      balance: 0,
      addressTo: '',
      amountTo: '',
      transactions: {
        totalNum: null,
        items: []
      },
      newAddress: ''
    }
  },
  watch: {
    addressWIF (val, oldVal) {
      let keyPair = bitcoin.ECPair.fromWIF(val, bitcoin.networks.testnet)
      this.address = keyPair.getAddress()
      axios.get(`${apiUrl}/addr/${this.address}/balance`)
      .then((response) => {
        this.balance = response.data / 100000000
      })
      .catch((error) => {
        console.log(error)
      })
    }
  },
  methods: {
    send () {
      alert(`HI`)
    },
    generateNewAddress () {
      let keyPair = bitcoin.ECPair.makeRandom({ network: bitcoin.networks.testnet })
     // let addr = keyPair.getAddress()
      let wifPair = keyPair.toWIF()
      this.newAddress = wifPair
    },
    refreshTransactions () {
      let params = {
        addrs: this.address,
        from: 0,
        to: 20
      }
      axios.post(`${apiUrl}/addrs/txs`, params)
      .then((response) => {
        this.transactions.items = response.data.items
        this.transactions.totalNum = response.data.totalNum
      })
      .catch((error) => {
        console.log(error)
      })
    }
  }
}

// // Put the object into storage
// localStorage.setItem('testObject', JSON.stringify(testObject));
// // Retrieve the object from storage
// var retrievedObject = localStorage.getItem('testObject');
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

.transaction{
  word-break: break-all;
}
</style>
