<template>
  <div :class="[prefixCls]">
    <i-menu
      :active-name="activeName"
      mode="vertical"
      :open-names="openNames">
      <template v-for="submenu in dataList">
        <i-menu-item
          :name="submenu.name"
          :to="{'name': submenu.name}"
          v-if="!submenu.children"
          :key="submenu.name">
          <i-icon :type="submenu.icon" v-if="submenu.icon" />
          {{ submenu.title }}
        </i-menu-item>
        <i-submenu
          :name="submenu.name"
          v-if="submenu.children"
          :key="submenu.title">
          <template slot="title">
            <i-icon :type="submenu.icon" v-if="submenu.icon" />
            <span>{{ submenu.title }}</span>
          </template>
          <template v-for="child in submenu.children">
            <i-menu-item
              :name="child.name"
              :to="{'name': child.name}"
              :key="child.name">
              {{ child.title }}
            </i-menu-item>
          </template>
        </i-submenu>
      </template>
    </i-menu>
  </div>
</template>
<script>
import { Menu, MenuItem, Submenu, Icon } from 'iview'

const prefixCls = 'kfc-sider'

export default {
	name: 'KfcSider',
	components: {
		'i-menu': Menu,
		'i-menu-item': MenuItem,
		'i-submenu': Submenu,
		'i-icon': Icon
	},
	props: {
		data: {
			type: Array,
			required: true,
			default: function () {
				return []
			}
		}
	},
	data () {
		return {
			dataList: this.data,
			activeName: '',
			openNames: [],
			prefixCls: prefixCls
		}
	},
	watch: {
		data (val) {
			this.dataList = val
			setTimeout(this.init, 0)
		}
	},
	mounted () {
		setTimeout(this.init, 0)
	},
	methods: {
		getParentName (name) {
			let result = null
			for (let i = 0; i < this.data.length; i++) {
				let dataChild = this.data[i]
				if (!dataChild.children) {
					continue
				}

				for (let j = 0; j < dataChild.children.length; j++) {
					if (dataChild.children[j].name === name) {
						result = dataChild.name
						return result
					}
				}
			}

			return result
		},

		init () {
			this.activeName = this.$router.currentRoute.name
			this.openNames = []

			if (this.activeName) {
				this.openNames.push(this.getParentName(this.activeName))
			}
		}
	}
}
</script>
