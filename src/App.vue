<template>
  <div class="container">
    <SearchBar @termChange="onTermChange"></SearchBar>
    <VideoList v-bind:videos="videos"></VideoList>
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar.vue";
import VideoList from "./components/VideoList.vue";

const API_KEY = "AIzaSyCeLPT4ONP80BKEOXCxjv1qX-1eA7OtV4k";
export default {
  name: "App",
  components: {
    SearchBar,
    VideoList,
  },
  data() {
    return { videos: [] };
  },
  methods: {
    onTermChange(searchTerm) {
      axios
        .get("https://www.googleapis.com/youtube/v3/search", {
          params: {
            key: API_KEY,
            type: "video",
            part: "snippet",
            q: searchTerm,
          },
        })
        .then((response) => {
          this.videos = response.data.items;
        });
    },
  },
};
</script>
