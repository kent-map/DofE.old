<template>
  <div id="main" :style="containerStyle">
    <div id="osd"></div>
  </div>
</template>

<script>

// https://cuberis.github.io/openseadragon-curtain-sync/

const prefixUrl = 'https://openseadragon.github.io/openseadragon/images/'

module.exports = {
  name: 've-compare',
  props: {
    items: { type: Array, default: () => ([]) },
    active: Boolean
  },
  data: () => ({
    viewerLabel: 'Image Compare',
    viewerIcon: 'fas fa-images',
    dependencies: ['https://cdn.jsdelivr.net/npm/openseadragon@2.4/build/openseadragon/openseadragon.min.js',
                   'https://cuberis.github.io/openseadragon-curtain-sync/src/openseadragon-curtain-sync.min.js'],
    viewer: null
  }),
  computed: {
    containerStyle() { return { height: this.active ? '100%' : '0' } },
    filteredItems() { return this.items.filter(item => item[this.$options.name]) },
    mode() { let itemsWithMode = this.filteredItems.filter(item => item.sync || item.curtain).map(item => item.sync ? 'sync' : 'curtain') 
             return itemsWithMode.length > 0 ? itemsWithMode[0] : 'curtain'
    },
    images() { return this.filteredItems
      .map((item, idx) => { return {
          key: `item-${idx}`,
          tileSource: { url: item.url, type: 'image', buildPyramid: true },
          shown: true
        }
      })
    }
  },
  mounted() { this.loadDependencies(this.dependencies, 0, this.init) },
  methods: {
    init() {
      console.log(`${this.$options.name}.init`)
      if (this.active) this.initViewer() 
    },
    initViewer() {
      let main = document.getElementById('main')
      let container = document.getElementById('osd')
      console.log(`initViewer: exists=${container !== null}`)
      if (container) {
        main.removeChild(container)
      }
      container = document.createElement('div')
      container.id = 'osd'
      container.style.height = '100%'
      main.appendChild(container)
      this.$nextTick(() => {
      this.viewer = new CurtainSyncViewer({
        mode: this.mode, // 'sync' or 'curtain'
        container,
        images: this.images,
        osdOptions: { // OpenSeaDragon options
          zoomPerClick: 2,
          homeFillsViewer: true,
        }
      })
      })
    }
  },     
  watch: {
    images() { if (this.active) this.initViewer() },
    active() { if (this.active) this.initViewer() },
    mode() { console.log(`mode=${this.mode}`) }
  }
}

</script>

<style>
</style>
