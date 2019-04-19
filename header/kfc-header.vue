<template>
  <i-header :class="[prefixCls]">
    <div :class="[prefixCls + '-logo']">
      <slot>
        <span>KFC</span>
      </slot>
    </div>
    <div :class="[prefixCls + '-menu']">
      <slot name="menu" />
    </div>
    <div :class="[prefixCls + '-userinfo']">
      <slot name="userinfo" />
    </div>
  </i-header>
</template>

<script>
import { Header } from 'iview'

const prefixCls = 'kfc-header'

export default {
  name: 'KfcHeader',
  components: {
    'i-header': Header
  },
  data () {
    return {
      prefixCls: prefixCls
    }
  }
}
</script>
