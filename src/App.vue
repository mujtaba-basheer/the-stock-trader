<template>
    <div class="container">
      <app-header></app-header>
      <div class="row">
        <div class="col-md-12">
          <router-view></router-view>
        </div>
      </div>
    </div>
</template>

<script>
    import Header from './components/Header';
    export default {
      data() {
        return {
          status: 'Critical'
        }
      },
      components: {
        appHeader: Header
      },
      created() {
        this.$store.dispatch('initStocks')
      },
    }
</script>

<style>
  body {
    padding: 30px;
  }
</style>
