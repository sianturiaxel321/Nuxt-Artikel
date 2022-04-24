<template>
  <div class="py-4">
    <div class="container">
      <div v-for="task in tasks" :key="task.id">
        <div
          class="item-task d-flex align-items-start pt-3 pb-4"
          v-if="task.id == paramId"
        >
          <input
            type="checkbox"
            name="status"
            id="task"
            class="me-2 mt-2"
            :checked="task.isDone"
            v-model="task.isDone"
          />
          <div>
            <div class="article-img col-12 d-none d-lg-block">
              <img :src="task.img" alt="#" />
            </div>
            <div class="title-task mb-1">
              {{ task.title }}
            </div>
            <div class="description-task small text-muted mb-3">
              {{ task.content }}
            </div>
          </div>
        </div>
      </div>
      <div class="action mt-4">
        <div
          class="btn btn-outline-secondary btn-sm mb-3"
          @click="$router.go(-1)"
        >
          Kembali
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        {
          id: 1,
          title: "Judul Artikel 1",
          content:
            "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Placeat dolor explicabo sint quos exercitationem fugiat reiciendis assumenda. Ad quia veritatis, dolor odit, voluptas numquam modi porro eius reprehenderit ullam tenetur?",
          img: "https://images.unsplash.com/photo-1649282806617-c51bb282899c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2070&q=80",
        },
        {
          id: 2,
          title: "Judul Artikel 2",
          content:
            "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Placeat dolor explicabo sint quos exercitationem fugiat reiciendis assumenda. Ad quia veritatis, dolor odit, voluptas numquam modi porro eius reprehenderit ullam tenetur?",
          img: "https://images.unsplash.com/photo-1649282806617-c51bb282899c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2070&q=80",
        },
        {
          id: 3,
          title: "Judul Artikel 3",
          content:
            "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Placeat dolor explicabo sint quos exercitationem fugiat reiciendis assumenda. Ad quia veritatis, dolor odit, voluptas numquam modi porro eius reprehenderit ullam tenetur?",
          img: "https://images.unsplash.com/photo-1649282806617-c51bb282899c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2070&q=80",
        },
        {
          id: 4,
          title: "Judul Artikel 4",
          content:
            "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Placeat dolor explicabo sint quos exercitationem fugiat reiciendis assumenda. Ad quia veritatis, dolor odit, voluptas numquam modi porro eius reprehenderit ullam tenetur?",
          img: "https://images.unsplash.com/photo-1649282806617-c51bb282899c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2070&q=80",
        },
      ],
      paramId: this.$route.params.id,
    };
  },
};
</script>
<style scoped>
.article-img img {
  width: 50%;
}
</style>
