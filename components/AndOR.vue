<template>
  <div class="and-or-template col-sm-10" :class=" isFirst ? 'and-or-first' : '' ">
    <div class="form-group and-or-top">
      <div class="col-sm-4">
        <button class="btn btn-xs btn-purple-outline btn-radius"
                :class=" isAnd ? 'btn-purple-outline-focus' : '' " @click.prevent="clickAnd">
          &nbsp;And&nbsp;
        </button>
        <button class="btn btn-xs btn-purple-outline btn-radius"
                :class=" !isAnd ? 'btn-purple-outline-focus' : '' " @click.prevent="clickOr">
          &nbsp;Or&nbsp;
        </button>
      </div>

      <div class="col-sm-8 btn-and-or">
        <button v-if="!isFirst" class="btn btn-xs btn-purple pull-right" @click.prevent="deleteSelf()">
          <i class="fa fa-fw fa-close"></i>
        </button>
        <button class="btn btn-xs btn-purple pull-right" @click.prevent="addGroup"> + ( group ) </button>
        <button class="btn btn-xs btn-purple add-rule pull-right" @click.prevent="addRule"> + add </button>
      </div>
    </div>

    <rule
      v-for="(rule, index) in rules" ref="rules"
      :options="options" :key="rule" @delete-rule="deleteRule(index)">
    </rule>

    <and-or
      class="and-or-offset"
      v-for="(group, index) in groups" ref="groups"
      :options="options" :key="group" @delete-group="deleteGroup(index)">
    </and-or>

  </div>
</template>

<script>
  import Rule from './Rule'

  export default {
    name: 'andOr',
    components: {
      Rule
    },
    props: {
      options: {
        type: Object,
        required: true
      },
      isFirst: {
        type: Boolean,
        default: false
      }
    },
    created () {
      this.addRule();
    },
    data () {
      return {
        isAnd: true,
        groups: [],
        rules: []
      }
    },
    methods: {
      clickAnd () {
        this.isAnd = true;
      },
      clickOr () {
        this.isAnd = false;
      },
      addRule () {
        var id = new Date().getTime();
        this.rules.push(id);
      },
      addGroup () {
        var id = new Date().getTime();
        this.groups.push(id);
      },
      deleteSelf () {
        this.$emit('delete-group');
      },
      deleteRule (index) {
        this.rules.splice(index, 1);
      },
      deleteGroup (index) {
        this.groups.splice(index, 1);
      },
      queryFormStatus () {
        var query = {};
        var rules = this.$refs.rules || {};
        var groups = this.$refs.groups || {};

        query.conditions = this.isAnd ? 'and' : 'or';
        query.rules = [];
        for(let i = 0; i < rules.length; i++){
          query.rules.push({
            //keyname: rules[i].keyname,
            keyid: rules[i].key,
            operater: rules[i].condition,
            value: rules[i].value
          })
        }
        for(let j = 0; j < groups.length; j++){
          query.rules[query.rules.length] = groups[j].queryFormStatus();
        }
        return query;
      }
    }
  }
</script>

<style>
  .and-or-template {
    padding: 8px;
    position: relative;
    border-radius: 3px;
    border: 1px solid #6d77b8;
    border-top: 3px solid #d2d6de;
    margin-bottom: 20px;
    /* width: 100%; */
    box-shadow: 0 1px 1px rgba(0,0,0,0.1);
    border-top-color: #6d77b8;
    background-color: rgba(217, 222, 255, 0.05);
  }

  .and-or-template:before,
  .and-or-template:after {
    content: '';
    position: absolute;
    left: -17px;
    width: 16px;
    height: calc(50% + 18px);
    border-color: #c0c5e2;
    border-style: solid;
  }

  .and-or-template:before {
    top: -18px;
    border-width: 0 0 2px 2px;
  }

  .and-or-template:after {
    top: 50%;
    border-width: 0 0 0 2px;
  }

  .and-or-first:before,
  .and-or-template:last-child:after {
    border: none;
  }

  .btn-and-or button{
    margin-left: 4px;
  }

  .and-or-offset {
    margin-left: 30px;
  }
</style>
