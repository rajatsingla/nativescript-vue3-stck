<script lang="ts" setup>
import { StackLayout, View } from '@nativescript/core';
import type { CollectionView } from '@nativescript-community/ui-collectionview';
import {
  ref,
  computed,
  onMounted,
  onUnmounted,
  $navigateTo,
} from 'nativescript-vue';
import Details from './Details.vue';

const counter = ref(0);
const collectionViewRef = ref();
const message = computed(() => {
  return `Blank {N}-Vue app: ${counter.value}`;
});

const htmlString = `
<h1 style="color: black; font-family: ui-sans-serif, system-ui;">
  <span style="color: #65adf1;">Html</span>View
</h1>`;

const story = ref({
  meta: {
    children: [],
  },
});

fetch('https://cheryl97.stck.me/api/r/101020/posts/229068')
  .then((response) => response.json())
  .then((r) => {
    story.value = r;
  })
  .catch((err) => {
    console.log(err);
  });
</script>

<template>
  <Frame>
    <Page actionBarHidden="true">
      <RootLayout>
        <GridLayout>
          <StackLayout>
            <!-- HEADER -->
            <FlexboxLayout class="justify-between mx-2">
              <Label text="more_horiz" class="m-icon-round text-center"></Label>
              <Label text="add" class="m-icon-round text-center"></Label>
            </FlexboxLayout>

            <!-- HEADER -->
            <GridLayout columns="*,  155" height="70" class="mx-2">
              <Label text="Cheryl" class="font-bold text-2xl"></Label>
            </GridLayout>

            <!-- ITEM LIST -->
            <CollectionView
              iosOverflowSafeArea="true"
              ref="collectionViewRef"
              class="px-1"
              height="100%"
              :items="story.meta.children"
              rowHeight="200"
              colWidth="50%"
            >
              <template #default="{ item, index }">
                <StackLayout
                  ~mainContent
                  class="mx-1 bg-secondary rounded-2xl py-3 my-1"
                  @tap="$navigateTo(Details, { props: { id: item.id } })" 
                  ignoreTouchAnimation="true"
                >
                  <Label
                    :text="item.title"
                    class="rounded-full text-center text-4xl"
                    height="68"
                    width="68"
                  />
                  <StackLayout class="ml-2 flex-col mt-1">
                    <Label
                      :text="item.title"
                      class="font-bold text-base text-center"
                    />
                  </StackLayout>
                  <GridLayout
                    horizontalAlignment="center"
                    columns="30,30,30,30,30"
                  >
                  </GridLayout>
                </StackLayout>
                <Stacklayout
                  ~rightDrawer
                  orientation="horizontal"
                  width="70"
                  class="text-center"
                >
                  <Label text="delete" class="m-icon-round text-center"></Label>
                </Stacklayout>
              </template>
            </CollectionView>
          </StackLayout>
        </GridLayout>
      </RootLayout>
    </Page>
  </Frame>
</template>

<style lang="scss" scoped>
.m-icon-round {
  font-family: 'Material Symbols Rounded', 'MaterialSymbolsRounded';
  font-weight: 100;
  font-size: 34;
}

.m-icon-outline {
  font-family: 'Material Symbols Outlined', 'MaterialSymbolsOutlined';
  font-weight: 100;
  font-size: 34;
}
</style>
