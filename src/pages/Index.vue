<template>
  <Layout>
    <div
      class="node-item"
      v-for="{ node } in $page.allNew.edges"
      :key="node.id"
    >
      <img :src="node.banner" alt="" />
      <div class="right">
        <h3>
          <g-link :to="'/new/' + node.id">
            <span>{{ node.title }}</span>
            <small> {{ node.date }} </small>
          </g-link>
        </h3>
        <p>{{ node.summary }}</p>
      </div>
    </div>
    <Pager :info="$page.allNew.pageInfo" />
  </Layout>
</template>

<page-query>
query ($page: Int) {
  allNew (perPage: 10, page: $page) @paginate {
    pageInfo {
      totalPages
      currentPage
    }
    edges {
      node {
        id
        title
        banner
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
    title: "最新动态",
  },
};
</script>

<style lang="less">
.node-item {
  margin-bottom: 30px;
  border-bottom: 1px solid #ebeef5;
  display: flex;
  justify-content: center;
  align-items: center;
  &:hover {
    h3 {
      a {
        color: #1e6bb8;
      }
    }
  }
  img {
    flex: none;
    width: 120px;
    border-radius: 4px;
    margin-right: 10px;
  }
  .right {
    flex: 1;
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
}
</style>
