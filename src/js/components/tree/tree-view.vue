<template>
  <div class="tree-view" :style="[tree_styles]">
    <logo />
    <button @click="build" class="build">Build</button>

    <div class="divider"></div>
    <tree-group
      type="globals"
      :add="false"
    />

    <tree-group
      type="styles"
      :add="true"
      :data="files.styles"
    />

    <tree-group
      type="templates"
      :add="true"
      :data="files.templates"
    />

    <tree-group
      type="partials"
      :add="true"
      :data="files.partials"
    />

  </div>
</template>

<!-- /////////////////////////////////////////////////////////////////////// -->

<script>
import { mapGetters } from 'vuex'
import { Request } from '@/utils'

export default {
  name: 'tree-view',
  mounted() {
    this.getFiles()
  },
  computed: {
    tree_styles() {
      return {
        width: this.sidebar_width + 'px'
      }
    },
    ...mapGetters([
      'files',
      'sidebar_width'
    ])
  },
  methods: {
    getFiles() {
      this.$store.dispatch('get_files')
    },
    async build() {
      const { data } = await Request('build', {
        method: 'post'
      })
      alert(data)
    }
  }
}
</script>

<!-- /////////////////////////////////////////////////////////////////////// -->

<style scoped lang="scss">
@import '~%/modules/colors';

.tree-view {
  position: relative;
  text-align: left;
  height: 100vh;
  width: 300px;
  float: left;
  background: $color-sidebar-background;
  color: $color-sidebar-color;
  white-space: nowrap;
  overflow-y: scroll;
  overflow-x: hidden;

  h3 {
    padding-left: 15px;
  }

  .logo {
    width: 120px;
    margin: 10px;
  }
}
.build {
  margin-top: 16px;
  float: right;
  margin-right: 16px;
}
.divider {
  width: 100%;
  height: 1px;
  background: #61656b;
}
</style>
