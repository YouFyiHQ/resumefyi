<script setup>
const props = defineProps({
  modelValue: {
    type: String,
    default: ''
  },
  minHeight: {
    type: String,
    default: '100px'
  }
})

const emit = defineEmits(['update:modelValue'])

const format = (command, value = null) => {
  document.execCommand(command, false, value)
  syncContent()
}

const syncContent = (event) => {
  const html = event?.target?.innerHTML ?? editorRef.value?.innerHTML ?? ''
  emit('update:modelValue', html)
}

const editorRef = ref(null)

const increaseFont = () => {
  document.execCommand('fontSize', false, '5')
  syncContent()
}

const decreaseFont = () => {
  document.execCommand('fontSize', false, '2')
  syncContent()
}

onMounted(() => {
  if (editorRef.value) {
    editorRef.value.innerHTML = props.modelValue || ''
  }
})

watch(
  () => props.modelValue,
  (val) => {
    if (editorRef.value && editorRef.value.innerHTML !== val) {
      editorRef.value.innerHTML = val || ''
    }
  }
)
</script>

<template>
  <div class="w-full">
    <div class="flex flex-wrap gap-2 mb-3">
      <button
        type="button"
        class="px-3 py-1 border rounded bg-white text-sm"
        @click="format('bold')"
      >
        B
      </button>

      <button
        type="button"
        class="px-3 py-1 border rounded bg-white text-sm italic"
        @click="format('italic')"
      >
        I
      </button>

      <button
        type="button"
        class="px-3 py-1 border rounded bg-white text-sm"
        @click="format('insertUnorderedList')"
      >
        Bullet
      </button>

      <button
        type="button"
        class="px-3 py-1 border rounded bg-white text-sm"
        @click="format('insertOrderedList')"
      >
        Number
      </button>

      <button
        type="button"
        class="px-3 py-1 border rounded bg-white text-sm"
        @click="increaseFont"
      >
        A+
      </button>

      <button
        type="button"
        class="px-3 py-1 border rounded bg-white text-sm"
        @click="decreaseFont"
      >
        A-
      </button>

      <button
        type="button"
        class="px-3 py-1 border rounded bg-white text-sm"
        @click="format('removeFormat')"
      >
        Clear
      </button>
    </div>

    <div
      ref="editorRef"
      contenteditable="true"
      class="w-full bg-transparent outline-none border-none p-0 text-[16px] leading-7 text-[#4b5563]"
      :style="{ minHeight }"
      @input="syncContent"
      @blur="syncContent"
    ></div>
  </div>
</template>