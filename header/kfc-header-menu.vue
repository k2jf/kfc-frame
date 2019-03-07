<template>
  <i-menu
    :active-name="activeName"
    mode="horizontal"
    theme="dark"
    width="auto"
    @on-select="onMenuSelect"
    :class="[prefixCls]"
  >
    <template v-for="submenu in data">
      <i-menu-item
        :name="submenu.name"
        v-if="!submenu.children"
        :key="submenu.name">
        <i-icon :type="submenu.icon" v-if="submenu.icon" />
        {{ submenu.title }}
      </i-menu-item>
    </template>
  </i-menu>
</template>
<script>
import { Menu, MenuItem, Submenu, Icon } from 'iview'

const prefixCls = 'kfc-header-memu-1'

export default {
  name: 'kfc-sider',
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
      activeName: '',
      prefixCls: prefixCls
		}
	},
  created () {
    let routeFullPath = this.$router.currentRoute.fullPath
    let matchedActiveName = this.getMachedActiveName(routeFullPath)
    if (matchedActiveName) {
      this.activeName = matchedActiveName
      this.$emit('on-select', matchedActiveName)
    }
  },
  methods: {
    getMachedActiveName (routeFullPath) {
      for (let i = 0; i < this.data.length; i++) {
        if ((routeFullPath + '/').indexOf('/' + this.data[i].name + '/') > -1) {
          return this.data[i].name
        }
      }

      return null
    },
    onMenuSelect (active) {
      let matchedRouter = this.getMatchedRouter(this.$router.options.routes, active)
      if (matchedRouter) {
        this.$router.push({path: matchedRouter.path})
        this.$emit('on-select', active)
      }
    },
    getMatchedRouter (routers, active) {
      let result = null
      for (let i = 0; i < routers.length; i++) {
        if ((routers[i].path + '/').indexOf('/' + active + '/') > -1) {
          result = routers[i]
          break
        }

        if (!routers[i].children) {
          continue
        }
        result = this.getMatchedRouter(routers[i].children, active)
        if (result) {
          break
        }
      }
      return result
    }
  }
}
</script>
