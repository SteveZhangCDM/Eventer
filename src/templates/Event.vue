<template>
  <Layout>
    <h1>{{ $page.event.title }}</h1>
    <img src="`http://localhost:1337${$page.event.thumbnail}`" alt="" />
    <p>{{ $page.event.description }}</p>
  </Layout>
</template>

<page-query>
query {
  event(id: "3"){
    id
    title
    duration
    price
    date
    thumbnail
    description
  }
}
</page-query>

<script>
export default {
  metaInfo() {
    return {
      title: this.$page.event.title,
    };
  },
};
</script>
