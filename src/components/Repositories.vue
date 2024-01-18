<script>
import axios from "axios";

export default {
  name: "Repositories",
  data() {
    return {
      repositories: [],
      currentPage: 1,
      itemsPerPage: 5,
    };
  },
  props: {
    style: {
      type: Object,
      required: true,
    },

    className: {
      type: String,
      required: true,
    },
  },
  computed: {
    paginatedRepositories() {
      const start = (this.currentPage - 1) * this.itemsPerPage;
      const end = start + this.itemsPerPage;
      return this.repositories.slice(start, end);
    },
    totalPages() {
      return Math.ceil(this.repositories.length / this.itemsPerPage);
    },
  },
  methods: {
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
  },
  mounted() {
    axios.get("https://api.github.com/users/Nicro01/repos").then((response) => {
      this.repositories = response.data;
    });
  },
};
</script>

<template>
  <div>
    <span
      v-for="(repo, index) in paginatedRepositories"
      :key="index"
      :class="className"
      :style="style"
    >
      <div class="col-span-1">
        <a :href="repo.html_url" target="_blank">{{ repo.name }}</a>
      </div>
      <div class="col-span-1">
        <p>{{ repo.description ?? "No Description" }}</p>
      </div>
    </span>
    <div
      className="font-bold grid grid-cols-3 mx-auto text-indigo-400 my-10"
      style="text-shadow: rgba(255, 255, 255, 0.113) 0px 0px 2px"
    >
      <button
        @click="prevPage"
        :disabled="currentPage === 1"
        :class="currentPage === 1 ? 'opacity-25' : 'opacity-100'"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="w-6 h-6"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M15.75 19.5 8.25 12l7.5-7.5"
          />
        </svg>
      </button>
      <span>{{ currentPage }} / {{ totalPages }}</span>
      <button
        @click="nextPage"
        :disabled="currentPage === totalPages"
        :class="currentPage === totalPages ? 'opacity-25' : 'opacity-100'"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="w-6 h-6"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="m8.25 4.5 7.5 7.5-7.5 7.5"
          />
        </svg>
      </button>
    </div>
  </div>
</template>
