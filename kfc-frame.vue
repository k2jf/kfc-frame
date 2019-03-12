<template>
  <div :class="[prefixCls]">
    <kfc-header>
      <kfc-header-menu
        :data="headerMenu"
        :sider-mapping="siderMenuMap"
        slot="menu"
        @on-select="onHeaderMenuSelect" />
      <kfc-header-userinfo slot="userinfo" />
    </kfc-header>
    <i-content>
      <kfc-sider :data="siderMenu" />
      <kfc-content />
    </i-content>
  </div>
</template>

<script>
import KFCHeader from './header/kfc-header.vue'
import KFCHeaderMenu from './header/kfc-header-menu.vue'
import KFCHeaderUserInfo from './header/kfc-header-userinfo.vue'

import { Content } from 'iview'
import KFCContent from './content/kfc-content.vue'
import KFCSider from './sider/kfc-sider.vue'

import { headerMenu, siderMenuMap, siderMenu } from '@/config/menu'

const prefixCls = 'kfc-frame'

export default {
	name: 'KfcFrame',
	components: {
		'kfc-header': KFCHeader,
		'kfc-header-menu': KFCHeaderMenu,
		'kfc-header-userinfo': KFCHeaderUserInfo,
		'i-content': Content,
		'kfc-sider': KFCSider,
		'kfc-content': KFCContent
	},
	data () {
		return {
			headerMenu: headerMenu,
			siderMenuMap: siderMenuMap,
			siderMenu: siderMenu,
			prefixCls: prefixCls
		}
	},
	methods: {
		onHeaderMenuSelect (siderMenu) {
			this.siderMenu = siderMenu
		}
	}
}
</script>
