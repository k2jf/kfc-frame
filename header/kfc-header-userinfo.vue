<template>
  <div :class="[prefixCls]">
    <i-avatar icon="ios-person" size="large" />
    <span :class="[prefixCls + '-name']">admin</span>
    <i-dropdown>
      <i-icon type="md-arrow-dropdown"></i-icon>
      <i-dropdown-menu slot="list">
        <i-dropdown-item @click.native="logout">退出</i-dropdown-item>
      </i-dropdown-menu>
    </i-dropdown>
  </div>
</template>

<script>
import { Avatar, Icon, Dropdown, DropdownMenu, DropdownItem } from 'iview'

const prefixCls = 'kfc-header-userinfo-1'

export default {
	name: 'kfc-header-userinfo-1',
	components: {
    'i-avatar': Avatar,
    'i-icon': Icon,
    'i-dropdown': Dropdown,
    'i-dropdown-menu': DropdownMenu,
    'i-dropdown-item': DropdownItem
	},
	data () {
		return {
      prefixCls: prefixCls
		}
	},
	mounted () {
	},
	methods: {
    logout () {
    }
	}
}
</script>
