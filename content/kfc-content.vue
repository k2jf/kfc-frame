<template>
  <i-content :class="[prefixCls]">
    <router-view />
  </i-content>
</template>

<script>
import { Content } from 'iview'

const prefixCls = 'kfc-content'

export default {
	name: 'kfc-content',
	components: {
		'i-content': Content
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
