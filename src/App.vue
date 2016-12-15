<template>
  <div class="col-xs-10 col-xs-offset-1" style="margin-top: 40px">
    <and-or :options="options" :isFirst="isFirst" ref="andOr"></and-or>

    <!--<button class="btn btn-purple" @click.prevent="fetchQuery">FetchQuery</button>-->
    <!--<button class="btn btn-purple" @click.prevent="fillQuery">FillQuery</button>-->
  </div>
</template>

<script>
  import AndOr from './components/AndOR'

export default {
  name: 'app',
  components: {
    AndOr
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

      isFirst: true
    }
  },

  methods: {
    fetchQuery () {
      console.log(this.$refs.andOr.queryFormStatus());
    }
  }
}
</script>

<style>
</style>
