<template>
  <div class="py-4">
    <div v-if="isLoading">
      <div class="lds-facebook">
        <div></div>
        <div></div>
        <div></div>
      </div>
    </div>
    <div class="container" v-else>
      <div class="title border-bottom">
        <div
          class="title border-bottom d-flex align-items-center justify-content-between py-2"
        >
          <h5>Artikel</h5>

          <div class="d-flex align-items-center ms-auto">
            <button
              class="btn btn-outline-primary py-1 px-3 me-4"
              @click="shuffle"
            >
              Shuffle!
            </button>
            <!-- /* Form input pencarian */ -->
            <input
              type="text"
              class="form-control"
              placeholder="Search"
              v-model="searchQuery"
            />
          </div>
        </div>
      </div>

      <transition-group name="artikel" tag="div" class="list-task row">
        <CardItem v-for="task in resultQuery" :key="task.id" :task="task" />
      </transition-group>
    </div>
  </div>
</template>
<script>
import CardItem from "@/components/Card/CardItem.vue";

export default {
  components: {
    CardItem,
  },

  data() {
    return {
      formAddTask: {
        title: "",
        content: "",
      },

      artikel: [
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
      isLoading: true,

      // Variabel penampung teks pencarian
      searchQuery: "",

      searchCategory: "",
      sortingBy: "",
      // Status saat menambahkan task
      isCreating: false,
      // Tipe layout daftar task
    };
  },
  beforeCreate() {
    console.log("before created");
  },
  created() {
    console.log(" created");
  },
  beforeMount() {
    console.log("beforeMount");
  },

  mounted() {
    setTimeout(() => {
      this.isLoading = false;
    }, 1000);
  },
  methods: {
    shuffle() {
      this.artikel = _.shuffle(this.artikel);
    },

    submitForm() {
      var myObj = {
        title: this.formAddTask.title,
        description: this.formAddTask.description,
        isDone: false,
        category: this.formAddTask.category,
        isHide: false,
      };
      // var myObj = {
      //   title: "Test Title 2",
      //   description: "Test Description 2",
      //   isDone: false,
      //   category: "Test Category 2",
      //   isHide: false,
      // };
      this.artikel.push(myObj);
      // console.log(this.artikel);
      return (
        (this.isCreating = false),
        (this.formAddTask.title = ""),
        (this.formAddTask.description = ""),
        (this.formAddTask.category = "")
      );
    },
  },
  computed: {
    resultQuery() {
      if (this.searchCategory) {
        return this.artikel.filter((item) => {
          return this.searchCategory
            .toLowerCase()
            .split(" ")
            .every((v) => item.category.toLowerCase().includes(v));
        });
      } else if (this.searchQuery) {
        return this.artikel.filter((item) => {
          return this.searchQuery
            .toLowerCase()
            .split(" ")
            .every((v) => item.title.toLowerCase().includes(v));
        });
      } else if (this.sortingBy) {
        // console.log("test");
        if (this.sortingBy == "asc") {
          return (this.artikel = _.orderBy(this.artikel, ["title"], ["asc"]));
          // console.log("asc");
        } else {
          return (this.artikel = _.orderBy(this.artikel, ["title"], ["desc"]));
          // console.log("desc");
        }
      } else {
        console.log(this.artikel);
        return this.artikel;
      }
    },
  },
};
</script>

<style>
.div h5 {
  font-family: sans;
  color: red;
}

.lds-facebook {
  display: inline-block;
  position: relative;
  width: 180px;
  height: 180px;
  top: 50%;
  left: 50%;
}
.lds-facebook div {
  display: inline-block;
  position: absolute;
  left: 8px;
  width: 16px;
  background: rgb(10, 9, 9);
  animation: lds-facebook 1.2s cubic-bezier(0, 0.5, 0.5, 1) infinite;
}
.lds-facebook div:nth-child(1) {
  left: 8px;
  animation-delay: -0.24s;
}
.lds-facebook div:nth-child(2) {
  left: 32px;
  animation-delay: -0.12s;
}
.lds-facebook div:nth-child(3) {
  left: 56px;
  animation-delay: 0;
}
@keyframes lds-facebook {
  0% {
    top: 8px;
    height: 64px;
  }
  50%,
  100% {
    top: 24px;
    height: 32px;
  }
}
#app .artikel-move {
  transition: 0.4s;
}
</style>
