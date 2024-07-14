<script lang="ts" setup>
import { ref, $navigateBack } from 'nativescript-vue';

const items = ref(
  Array(1000)
    .fill(0)
    .map((_, index) => `Item ${index + 1}`),
);

const { id } = defineProps({
  id: {
    type: Number,
    required: true
  }
});

const chapter = ref({});

fetch(`https://cheryl97.stck.me/api/r/101020/posts/${id}`)
  .then((response) => response.json())
  .then((r) => {
    chapter.value = r;
  })
  .catch((err) => {
    console.log(err);
  });
</script>

<template>
  <Page actionBarHidden="true">
    <GridLayout rows="auto, *">
      <FlexboxLayout class="mx-2">
        <Label
          :text="`Back`"
          @tap="$navigateBack"
          class=""
        />
        <Label :text="chapter.title" class="text-center px-4 py-10 text-2xl text-gray-900 font-bold"></Label>
      </FlexboxLayout>

     

      <ContentView row="1" class="">
        <HtmlView class="text-xl m-4" :html="chapter.content" />
      </ContentView>
    </GridLayout>
  </Page>
</template>
