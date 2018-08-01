<template>
    <layout layout-style="pulled-left" layout-content="no-container">
        <graphic-builder
                v-if="activeTab === 'create'"
                v-on:tabChange="changeTab"
                :selectedAssetPacks="selectedAssetPacks" />
        <asset-picker
                v-if="activeTab === 'picker'"
                v-on:tabChange="changeTab"
                v-on:pickAsset="toggleAsset"
                :selectedAssetPacks="selectedAssetPacks" />
    </layout>
</template>

<script>
  import AssetPicker from './AssetPicker/AssetPicker.vue';
  import GraphicBuilder from './GraphicBuilder/GraphicBuilder.vue';

  export default {
    name: 'CreateGraphic',
    components: {
      GraphicBuilder,
      AssetPicker
    },
    data: () => ({
      activeTab: 'create',
      selectedAssetPacks: [],
    }),
    methods: {
      changeTab(tab) {
        this.activeTab = tab;
      },
      toggleAsset(asset) {
        const index = this.selectedAssetPacks.findIndex(item => item.id === asset.id);
        if (index >= 0) {
          return this.selectedAssetPacks = [
            ...this.selectedAssetPacks.slice(0, index),
            ...this.selectedAssetPacks.slice(index + 1),
          ];
        }
        this.selectedAssetPacks.push(asset);
      }
    },
  };
</script>

<style scoped lang="scss">
    .create-art-wrapper {
        background-color: #D9D9D9;
        min-height: calc(100vh - 70px);
        position: relative;
        width: 1280px;
        margin: 0 auto;
        left: -80px;

        &.create {
            display: flex;
        }

        .create-container {
            padding: 40px 0;
            box-sizing: border-box;
            margin-right: 0;
            overflow: hidden;
        }

        @media all and (max-width: 1280px) {
            width: 100%;
            left: 0;
            .create-container {
                margin-right: auto;
            }
        }
    }
</style>