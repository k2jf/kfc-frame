<template>
  <div :class="[prefixCls]">
    <kfc-header>
      <kfc-header-menu
      :data="headerMenu"
      :sider-mapping="siderMenuMap"
      @on-select="onHeaderMenuSelect"
      slot="menu" />
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

const prefixCls = 'kfc-frame'

export default {
	name: 'kfc-frame',
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
      headerMenu: [
      ],
      siderMenuMap: null,
      siderMenu: [{
        name: 'dataset.list',
        icon: 'md-person',
        title: '数据列表'
      },
      {
        name: 'dataset.create',
        icon: 'md-person',
        title: '数据创建'
      },
      {
        name: 'dataset.edit',
        icon: 'md-person',
        title: '数据编辑'
      }],
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
