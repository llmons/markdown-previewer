<script setup lang="ts">
import { onMounted, ref } from 'vue'
import markdownit from 'markdown-it'
import ThemeSwap from '@/components/ThemeSwap.vue'

const text = ref(`# h1 Heading
## h2 Heading
### h3 Heading
#### h4 Heading
##### h5 Heading
###### h6 Heading
`)
const marked = ref('')

const md = markdownit({
  breaks: true,
});

const updateText = () => {
  marked.value = md.render(text.value);
}

onMounted(() => {
  updateText();
})
</script>

<template>
  <div class="flex flex-col h-screen gap-5">
    <!-- navabr -->
    <div class="flex items-center justify-center text-4xl navbar">
      <div class="flex items-center navbar-center">
        Markdown Previewer
      </div>
      <div class="flex items-center navbar-end">
        <ThemeSwap />
      </div>
    </div>

    <!-- editor & previewer -->
    <div class="container flex items-center justify-center h-full mx-auto">
      <textarea
        class="w-1/2 h-full p-4 text-lg border-2 rounded-lg resize-none textarea textarea-ghost focus:outline-none border-base-300 focus:border-2 focus:border-base-300"
        v-model="text" @input="updateText"></textarea>
      <div class="divider divider-horizontal"></div>
      <div class="w-1/2 h-full p-4 prose border-2 rounded-lg border-base-300" v-html="marked"></div>
    </div>
  </div>
</template>
