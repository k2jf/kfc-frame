<template>
  <i-header :class="[prefixCls]">
    <div :class="[prefixCls + '-logo']">
      <slot>
        <img :class="[prefixCls + '-logo-img']" src="@/assets/logo.png" />
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
	name: 'kfc-header',
	components: {
		'i-header': Header
	},
	data () {
		return {
      prefixCls: prefixCls
		}
	},
	mounted () {
	},
	methods: {
	}
}
</script>
