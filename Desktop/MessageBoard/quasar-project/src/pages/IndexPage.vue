<template>
  <q-page class="row items-center justify-evenly">
    <div id="q-app" style="min-height: 100vh">
      <div class="q-pa-md example-masonry">
        <!--q-btn class="q-mb-md" color="primary" label="Regenerate layout" @click="() => console.log('click')"></q-btn-->

        <div class="column example-container">
          <div class="flex-break hidden"></div>
          <div class="flex-break"></div>
          <div class="flex-break"></div>
          <div class="flex-break"></div>

          <div
            v-for="post in posts"
            :key="post"
            class="example-cell"
            tabindex="0"
          >
            <q-card class="bg-secondary text-white">
              <div class="text-h4 q-pa-sm">{{ post.title }}</div>
              <q-separator/>
              <div class="q-pa-md">{{ post.text }} </div>
            </q-card>
          </div>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { Todo, Meta } from "components/models";
import ExampleComponent from "components/ExampleComponent.vue";
import { ref } from "vue";
import { Environment, RCA } from "src/Classes";

let posts: any[];
const posts_stringified = localStorage.getItem("posts");
if (!posts_stringified) posts = [];
else posts = JSON.parse(posts_stringified);

class MessageRCA extends RCA {
  public onControl(source_temp_id: string, action_info: any): void {
    console.log(action_info);
    posts = posts.concat([action_info]);
    console.log(posts);
    localStorage.setItem("posts", JSON.stringify(posts));
  }
  public generateTempId(): string {
    return "specific_ctrlr_not_important";
  }

  public acceptNewController(): Boolean {
    return true;
  }
}
const demoRCA = new MessageRCA(
  "https://test-igrica.onrender.com/",
  "pristupni_kod"
);
</script>
<style lang="sass">
.example-masonry
  .flex-break
    flex: 1 0 100% !important
    width: 0 !important

  $x: 4

  @for $i from 1 through ($x - 1)
    .example-container > div:nth-child(#{$x}n + #{$i})
      order: #{$i}

  .example-container > div:nth-child(#{$x}n)
    order: #{$x}

  .example-container
    height: 700px

    .example-cell
      width: 25%
      padding: 1px

      > div
        padding: 4px 8px
        box-shadow: inset 0 0 0 2px #9e9e9e
</style>
