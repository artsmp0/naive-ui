<markdown>
# 自定义 key 和 label 的字段

后端会传来各种各样的数据。
</markdown>

<template>
  <n-tree
    block-line
    :data="data"
    :default-expanded-keys="defaultExpandedKeys"
    key-field="whateverKey"
    label-field="whateverLabel"
    children-field="whateverChildren"
    selectable
    ignore-empty-children
  />
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import { repeat } from 'seemly'
import { TreeOption } from 'naive-ui'

function createData (level = 4, baseKey = ''): TreeOption[] | undefined {
  if (!level) return []
  return repeat(6 - level, undefined).map((_, index) => {
    const key = '' + baseKey + level + index
    return {
      whateverLabel: createLabel(level),
      whateverKey: key,
      whateverChildren: createData(level - 1, key)
    }
  })
}

function createLabel (level: number): string {
  if (level === 4) return '道生一'
  if (level === 3) return '一生二'
  if (level === 2) return '二生三'
  if (level === 1) return '三生万物'
  return ''
}

export default defineComponent({
  setup () {
    return {
      data: createData(),
      defaultExpandedKeys: ref(['40', '41'])
    }
  }
})
</script>
