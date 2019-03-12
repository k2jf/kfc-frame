<template>
  <i-content :class="[prefixCls]">
    <router-view />
  </i-content>
</template>

<script>
import { Content } from 'iview'

const prefixCls = 'kfc-content'

export default {
	name: 'KfcContent',
	components: {
		'i-content': Content
	},
	data () {
		return {
			prefixCls: prefixCls
		}
	}
}
</script>
