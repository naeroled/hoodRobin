<template>
<nav class="navbar navbar-default">
  <div class="container-fluid">
    <div class="navbar-header">
        <router-link to="/" class="navbar-brand">hoodRobin</router-link>
    </div>

    <div class="collapse navbar-collapse">
      <ul class="nav navbar-nav">
        <router-link to="/portfolio" activeClass="active" tag="li"><a>Portfolio</a></router-link>
        <router-link to="/stocks" activeClass="active" tag="li"><a>Stocks</a></router-link>
      </ul>
      <strong class="navbar-text navbar-right funds">Funds: {{ funds | currency }}</strong>
      <ul class="nav navbar-nav navbar-right">
        <li><a href="#" @click="endDay">End Day</a></li>
        <li 
            class="dropdown" 
            :class="{open: isDropdownOpen}"
            @click="isDropdownOpen = !isDropdownOpen"
            >
          <a 
          href="#" 
          class="dropdown-toggle" 
          data-toggle="dropdown" 
          role="button" 
          aria-haspopup="true" 
          aria-expanded="false">Save & Load
          <span class="caret"></span></a>
          <ul class="dropdown-menu">
            <li><a href="#" @click="saveData">Save Data</a></li>
            <li><a href="#" @click="loadData">Load Data</a></li>
          </ul>
        </li>
      </ul>
    </div><!-- /.navbar-collapse -->
  </div><!-- /.container-fluid -->
</nav>
</template>

<script>
import {mapActions} from 'vuex';
export default {
    data() {
        return {
            isDropdownOpen: false,
        }
    },
    computed: {
        funds() {
            return this.$store.getters.funds;
        }
    },
    methods: {
        ...mapActions({
            randomizeStocks : 'randomizeStocks',
            fetchData: 'loadData'
        }),
        endDay() {
            this.randomizeStocks();

        },
        saveData() {
            const data = {
                funds: this.$store.getters.funds,
                stockPortfolio: this.$store.getters.stockPortfolio,
                stocks: this.$store.getters.stocks
            };
            this.$http.put('data.json', data);
        },
        loadData() {
            this.fetchData();

        }
    }
}
</script>

<style>
.navbar {
    /* background-color: #1B1B1D; */
    color: white !important;
    box-shadow: 0 10px 6px -6px #777;
    border: none;
    margin-bottom: 30px;

}

.navbar-brand {
    color: #20CE99 !important;
}

.funds {
    color: #20CE99 !important;
}
</style>

