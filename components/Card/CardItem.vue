<template>
  <div
    :class="[
      'item-task d-flex align-items-start border-bottom pt-3 pb-4',
      isGrid ? 'col-12 col-md-6 col-lg-4' : 'col-12',
    ]"
  >
    <input
      type="checkbox"
      name="status"
      id="task"
      class="me-2 mt-2"
      :checked="task.isDone"
      v-model="task.isDone"
    />

    <div v-show="!isHide">
      <div class="article-img col-12 d-none d-lg-block">
        <img :src="task.img" alt="#" />
      </div>
      <div class="description-task small text-muted">
        {{ task.title }}
      </div>
      <div class="description-task small text-muted">
        {{ task.content }}
      </div>
      <nuxt-link class="title-task mb-1" :to="'app/detail/' + task.id">
        Read More
      </nuxt-link>
    </div>
    <span v-show="isHide">Task Selesai</span>
  </div>
</template>

<script>
export default {
  props: {
    task: {
      type: Object,
      default: "Untitled",
    },
    isHide: {
      type: Boolean,
      required: true,
      default: false,
    },
    isGrid: {
      type: Boolean,
      required: true,
      default: false,
    },
  },
};
</script>
<style scoped>
.article-img img {
  width: 50%;
}
</style>
