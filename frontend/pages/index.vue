<template>
  <div>
    <Heading
      :title="props.global.siteName"
      :description="props.global.siteDescription"
    />
    <main>
      <div class="grid grid-cols-3 gap-10">
        <div v-for="article in articlesList">
          <img
            class="object-cover w-full"
            src="https://www.placeholder.co/300x300"
            alt=""
          />
          <div>
            <h2>{{ article.attributes.title }}</h2>
            <p>{{ article.attributes.description }}</p>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup lang="ts">
const props = defineProps({
  global: Object,
});

const { find } = useStrapi4();
const { data: articlesList, error } = await useAsyncData(
  "articles",
  () => find("articles"),
  {
    populate: "deep",
    transform: (articlesList) => {
      return articlesList.data;
    },
  }
);
</script>

<style>
body {
  margin: 0;
}
</style>
