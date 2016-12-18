<template>
  <div class="modal" v-show="show">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <button type="button" class="close" data-dismiss="modal" aria-label="Close" @click="handle('close')">
            <span aria-hidden="true">×</span>
          </button>
          <slot name="header">
            <h4 class="modal-title">Default Modal</h4>
          </slot>
        </div>

        <form class="form-horizontal" role="form">
        <div class="modal-body">
          <slot name="body">
            <p>One fine body…</p>
          </slot>
        </div>
        <div class="modal-footer">
          <slot name="footer">
            <button type="button" class="btn btn-default" @click="handle('cancel')">Cancel</button>
            <button type="button" class="btn btn-info" @click="handle('confirm')">OK</button>
          </slot>
        </div>
        </form>

      </div>
      <!-- /.modal-content -->
    </div>
    <!-- /.modal-dialog -->
  </div>
</template>

<script>
  export default {
    name: 'modal',
    props: {
      show: {
        type: Boolean,
        required: true
      }
    },
    data () {
      return {}
    },
    computed: {},
    methods: {
      handle (type) {
        switch (type){
          case 'close':
          case 'cancel':
            this.$emit('hide');
            break;
          case 'confirm':
            this.$emit('confirm');
            break;
        }
      }
    }
  }
</script>

<style>
  .modal {
    display: block;
  }
</style>
