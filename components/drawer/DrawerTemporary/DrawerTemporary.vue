<template>
  <aside
    class="mdc-drawer mdc-drawer--temporary"
    @MDCTemporaryDrawer:close="model = false">
    <nav class="mdc-drawer__drawer">
      <slot name="toolbarSpacer"/>
      <slot name="header"/>
      <slot />
    </nav>
  </aside>
</template>

<script>
import { MDCTemporaryDrawer } from '@material/drawer'

import { baseComponentMixin, themeClassMixin } from '../../base'

export default {
  mixins: [baseComponentMixin, themeClassMixin],
  model: {
    prop: 'open',
    event: 'change'
  },
  props: {
    open: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      mdcTemporaryDrawer: undefined
    }
  },
  computed: {
    model: {
      get () {
        return this.open
      },
      set (value) {
        this.$emit('change', value)
      }
    }
  },
  watch: {
    open () {
      this.mdcTemporaryDrawer.open = this.open
    }
  },
  mounted () {
    this.mdcTemporaryDrawer = MDCTemporaryDrawer.attachTo(this.$el)
    this.mdcTemporaryDrawer.open = this.open
  },
  beforeDestroy () {
    this.mdcTemporaryDrawer.destroy()
  }
}
</script>
