<template>
  <SmartModal v-if="show" @close="$emit('hide-modal')">
    <template #header>
      <h3 class="heading">{{ $t("edit_folder") }}</h3>
      <div>
        <button class="icon button" @click="hideModal">
          <i class="material-icons">close</i>
        </button>
      </div>
    </template>
    <template #body>
      <label for="selectLabelGqlEditFolder">{{ $t("label") }}</label>
      <input
        id="selectLabelGqlEditFolder"
        v-model="name"
        class="input"
        type="text"
        :placeholder="folder.name"
        @keyup.enter="editFolder"
      />
    </template>
    <template #footer>
      <span></span>
      <span>
        <button class="icon button" @click="hideModal">
          {{ $t("cancel") }}
        </button>
        <button class="icon button primary" @click="editFolder">
          {{ $t("save") }}
        </button>
      </span>
    </template>
  </SmartModal>
</template>

<script lang="ts">
import Vue from "vue"
import { editGraphqlFolder } from "~/newstore/collections"

export default Vue.extend({
  props: {
    show: Boolean,
    folder: { type: Object, default: () => {} },
    folderPath: { type: String, default: null },
  },
  data() {
    return {
      name: null,
    }
  },
  methods: {
    editFolder() {
      editGraphqlFolder(this.folderPath, { ...this.folder, name: this.name })
      this.hideModal()
    },
    hideModal() {
      this.name = null
      this.$emit("hide-modal")
    },
  },
})
</script>
