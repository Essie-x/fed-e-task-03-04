<template>
  <Layout>
    <div
      class="node-item"
      v-for="{ node } in $page.allPost.edges"
      :key="node.id"
    >
      <h3>
        <g-link :to="'/blog/' + node.id">
          <span>{{ node.title }}</span>
          <small> {{ node.date }} </small>
        </g-link>
      </h3>
      <p>{{ node.summary }}</p>
    </div>
    <Pager :info="$page.allPost.pageInfo" />
  </Layout>
</template>

<page-query>
query ($page: Int) {
  allPost (perPage: 10, page: $page) @paginate {
    pageInfo {
      totalPages
      currentPage
    }
    edges {
      node {
        id
        title
        date
        summary
      }
    }
  }
}
</page-query>

<script>
import { Pager } from "gridsome";

export default {
  components: {
    Pager,
  },
  metaInfo: {
    title: "博客列表",
  },
};
</script>

<style lang="less">
.node-item {
  margin-bottom: 30px;
  border-bottom: 1px solid #ebeef5;
  &:hover {
    h3 {
      a {
        color: #1e6bb8;
      }
    }
  }
  h3 {
    font-size: 1.1rem;
    a {
      color: #333;
    }
    small {
      font-size: 12px;
      color: gray;
      padding: 0 10px;
    }
  }
  p {
    font-size: 0.9rem;
  }
}
</style>
