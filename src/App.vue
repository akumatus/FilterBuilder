<template>
  <div>
    <h1 class="title">
      <img src="./assets/logo.png" class="logo">
      Vue-Filter-Builder
      <small class="version"></small>
    </h1>

    <div class="col-xs-8 col-xs-offset-2" style="margin-top: 40px">
      <and-or :options="options" :isFirst="isFirst" ref="andOr"></and-or>

      <div class="pull-right">
        <button class="btn btn-warning" @click.prevent="resetFilter">Reset Filter</button>
        <button class="btn btn-success" @click.prevent="fetchQuery">Fetch Query</button>
        <button class="btn btn-info" @click.prevent="showModal">Fill Query</button>
      </div>
    </div>

    <modal :show="showQueryModal" @hide="showQueryModal = false" @confirm="showQueryModal = false">
      <h4 class="modal-title" slot="header">Fetch Query</h4>
      <div class="box-body" slot="body">
        <pre class="filter-fetched-query">{{fetchedQuery}}</pre>
      </div>
    </modal>

    <modal :show="showFillModal" @hide="showFillModal = false" @confirm="fillQuery">
      <h4 class="modal-title" slot="header">Fill Query</h4>
      <div class="box-body" slot="body">
        <textarea class="filter-filled-query" v-model="filledQuery"></textarea>
      </div>
    </modal>
  </div>
</template>

<script>
  import AndOr from './components/AndOR'
  import Modal from './components/Modal.vue'


  export default {
    name: 'app',
    components: {
      AndOr, Modal
    },
    data () {
      return {
        options: {
          keys: [{
            name: 'Choose Key',
            id: -99
          },{
            name: 'Crash Number',
            id: 134
          },{
            name: 'GUID',
            id: 87
          },{
            name: 'Daily Startup',
            id: 256
          },{
            name: 'IP',
            id: 121
          }],

          operators: [{
            name: 'Choose Operator',
            id: -99
          },{
            name: 'more',
            id: '>'
          },{
            name: 'equal',
            id: '='
          },{
            name: 'less',
            id: '<'
          }]
        },

        isFirst: true,

        showQueryModal: false,

        showFillModal: false,

        fetchedQuery: '',

        filledQuery: ''
      }
    },

    mounted () {
      this.$nextTick(function () {
        this.init()
      });
    },

    methods: {
      init () {
        this.$refs.andOr.addRule();
        this.$refs.andOr.addGroup();
        this.$refs.andOr.addGroup();
      },

      fetchQuery () {
        this.showQueryModal = true;
        this.fetchedQuery = JSON.stringify(this.$refs.andOr.queryFormStatus(), null, 4);
      },

      fillQuery () {
        var query = JSON.parse(this.filledQuery);
        this.$refs.andOr.fillFormStatus(query);
        this.showFillModal = false;
      },

      showModal () {
        this.showFillModal = true;
        this.filledQuery = '';
      },

      resetFilter () {
        this.$refs.andOr.groups = [];
        this.$refs.andOr.rules = [];
      }
    }
  }
</script>

<style>
  body {
    background: linear-gradient(to left bottom, rgb(179, 213, 255) 0%, rgb(255, 183, 179) 100%);
  }

  .title {
    text-align: center;
    margin-top: 80px;
  }

  .logo {
    height: 4.375rem;
    margin-right: 1.25rem;
    vertical-align: middle;
    display: inline-block;
  }

  .filter-fetched-query {
    max-height: 460px;
  }

  .filter-filled-query {
    width: 100%;
    height: 460px;
  }
</style>
