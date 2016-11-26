<template>
  <div class="form-group and-or-rule">
    <div class=" col-sm-3">
      <select class="form-control input-sm" v-model="key">
        <option v-for="option in options.keys.options" :value="option.key">
          {{option.name}}
        </option>
      </select>
    </div>

    <div class="col-sm-3">
      <select class="form-control input-sm" v-model="condition">
        <option v-for="option in options.conditions.options" :value="option.value">
          {{option.name}}
        </option>
      </select>
    </div>

    <div class="col-sm-3">
      <label class="sr-only">Value</label>
      <input type="text" class="form-control input-sm" v-model="value" placeholder="Value">
    </div>

    <button class="btn btn-xs btn-purple-outline btn-radius btn-purple-round" @click.prevent="deleteSelf()">
      <i class="fa fa-fw fa-close"></i>
    </button>
  </div>
</template>

<script>
  export default {
    name: 'rule',
    props: ['options'],
    watch: {
      'options.keys.options' () {
        this.key = -99;
      },
      'options.conditions.options' () {
        this.condition = -99;
      }
    },
    data () {
      return {
        key: -99,
        condition: -99,
        value: ''
      }
    },
    methods: {
      deleteSelf () {
        this.$emit('delete-rule');
      }
    }
  }
</script>

<style>
  .and-or-rule {
    position: relative;
    height: 30px;
    margin-left: 15px !important;
  }

  .and-or-rule:before,
  .and-or-rule:after {
    content: '';
    position: absolute;
    left: -1px;
    width: 16px;
    height: calc(50% + 15px);
    border-color: #c0c5e2;
    border-style: solid;
  }

  .and-or-rule:before {
    top: -15px;
    border-width: 0 0 2px 2px;
  }

  .and-or-rule:after {
    top: 50%;
    border-width: 0 0 0 2px;
  }

  .and-or-rule:last-child:after {
    border: none;
  }
</style>
