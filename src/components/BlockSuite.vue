<script setup lang="ts">
import '@blocksuite/editor/themes/affine.css'
import { AffineSchemas, __unstableSchemas } from '@blocksuite/blocks/models'
import { Workspace } from '@blocksuite/store'
import { onMounted, ref } from 'vue'
import { EditorContainer } from '@blocksuite/editor'

const workspace = new Workspace({
  id: 'test'
})
workspace.register(AffineSchemas).register(__unstableSchemas)
const page = workspace.createPage('page0')
const pageBlockId = page.addBlock('affine:page', {
  title: new page.Text('')
})
page.addBlock('affine:surface', {}, null)
const frameId = page.addBlock('affine:frame', {}, pageBlockId)
page.addBlock('affine:paragraph', {}, frameId)

const dom = ref<HTMLElement>()
onMounted(function () {
  const editor = new EditorContainer()
  editor.autofocus = true
  editor.page = page
  dom.value?.appendChild(editor)
})
</script>

<template>
  <div ref="dom">
  </div>
</template>
