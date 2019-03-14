<template>
  <i-menu
    :active-name="activeName"
    mode="horizontal"
    theme="dark"
    width="auto"
    :class="[prefixCls]"
    @on-select="onMenuSelect">
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
import { Menu, MenuItem, Icon } from 'iview'

const prefixCls = 'kfc-header-memu-1'

export default {
  name: 'KfcHeaderMenu',
  components: {
    'i-menu': Menu,
    'i-menu-item': MenuItem,
    'i-icon': Icon
  },
  props: {
    data: {
      type: Array,
      required: true,
      default: function () {
        return []
      }
    },
    siderMapping: {
      type: Object,
      default: null
    }
  },
  data () {
    return {
      activeName: '',
      prefixCls: prefixCls
    }
  },
  created () {
    // 无子菜单
    if (!this.siderMapping) {
      this.activeName = this.$router.currentRoute.name
      return
    }
    // 有子菜单
    for (let index in this.siderMapping) {
      let value = this.siderMapping[index]
      if (this.siderMenusRouteMatched(value)) {
        this.activeName = index
        this.$emit('on-select', value)
        break
      }
    }
  },
  methods: {
    onMenuSelect (active) {
      if (!this.siderMapping) {
        this.$router.push({ name: active })
        return
      }

      this.$router.push({ name: this.siderMapping[active][0].name })
      this.$emit('on-select', this.siderMapping[active])
    },
    siderMenusRouteMatched (menu) {
      for (let i = 0; i < menu.length; i++) {
        if (menu[i].name === this.$router.currentRoute.name) {
          return true
        }

        let children = menu[i].children
        if (!children) {
          continue
        }

        for (let j = 0; j < children.length; j++) {
          if (children[j].name === this.$router.currentRoute.name) {
            return true
          }
        }
      }

      return false
    }
  }
}
</script>
