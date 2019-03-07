<template>
  <div :class="[prefixCls]">
    <kfc-header>
      <kfc-header-menu
      :data="headerMenu"
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
        {
          name: 'dataset',
          icon: 'md-person',
          title: '数据管理'
        },
        {
          name: 'model',
          icon: 'md-person',
          title: '模型管理'
        }
      ],
      siderMenuMap: {
        'dataset': [
          {
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
          }
        ],
        'model': [
          {
            name: 'model.list',
            icon: 'md-person',
            title: '模型列表'
          },
          {
            name: 'model.edit',
            icon: 'md-person',
            title: '模型编辑'
          }
        ]
      },
      siderMenu: [],
      prefixCls: prefixCls
		}
	},
	mounted () {
	},
	methods: {
    onHeaderMenuSelect (activeHeaderMenuName) {
      this.siderMenu = this.siderMenuMap[activeHeaderMenuName]
    }
	}
}
</script>
