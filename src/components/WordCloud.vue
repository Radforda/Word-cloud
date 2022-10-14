<script setup>
import { ref } from "vue";
const words = [
  "Avatar",
  "Star",
  "Wars",
  "Force",
  "Awakens",
  "Jurassic",
  "World",
  "Star",
  "Wars",
  "Last",
  "Jedi",
  "Jurassic",
  "World",
  "Fallen",
  "Kingdom",
  "Transformers",
  "Dark",
  "Moon",
  "Transformers",
  "Age",
  "Extinction",
  "Star",
  "Wars",
  "Rise",
  "Skywalker",
  "Rogue",
  "One",
  "Star",
  "Wars",
  "Story",
  "Jurassic",
  "Park",
  "Star",
  "Wars",
  "Phantom",
  "Menace",
  "Jurassic",
  "World",
  "Dominion",
  "Jumanji",
  "Welcome",
  "Jungle",
  "Hunger",
  "Games",
  "Catching",
  "Fire",
  "Star",
  "Wars",
  "Revenge",
  "Sith",
  "Ni",
  "Hao",
  "Li",
  "Huan",
  "Ying",
  "Transformers",
  "Revenge",
  "Fallen",
  "Independence",
  "Day",
  "Jumanji",
  "Next",
  "Level",
  "E.T.",
  "Extra-Terrestrial",
  "Star",
  "Wars",
  "New",
  "Hope",
  "Hunger",
  "Games",
  "Mockingjay",
  "Part",
  "1",
  "2012",
  "Matrix",
  "Reloaded",
  "Inception",
  "Dawn",
  "Planet",
  "Apes",
  "Transformers",
  "Liu",
  "Lang",
  "Di",
  "Qiu",
  "Hunger",
  "Games",
  "Star",
  "Wars",
  "Attack",
  "Clones",
  "Men",
  "Black",
  "3",
  "Martian",
  "Interstellar",
  "Hunger",
  "Games",
  "Mockingjay",
  "Part",
  "2",
  "Lost",
  "World",
  "Jurassic",
  "Park",
  "War",
  "Worlds",
  "Transformers",
  "Last",
  "Knight",
  "Men",
  "Black",
  "I",
  "Am",
  "Legend",
  "Ready",
  "Player",
  "One",
  "Kong",
  "Skull",
  "Island",
  "Day",
  "After",
  "Tomorrow",
  "Armageddon",
  "Star",
  "Wars",
  "Empire",
  "Strikes",
  "Back",
  "WALL-E",
  "World",
  "War",
  "Z",
  "Godzilla",
  "Meg",
  "Mei",
  "Ren",
  "Yu",
  "Terminator",
  "2",
  "Judgment",
  "Day",
];
const createWordCloud = (words) => {
  let wordCloud = {};
  let maxCount = 0;
  let minCount = 1;
  let maxFont = 50;
  let minFont = 12;
  let colorNumber = 0;
  let colors = ["blue", "green", "red", "orange", "purple"];

  words.forEach((title) => {
    title = title.split(" ");
    title.forEach((word) => {
      if (!wordCloud[word]) {
        wordCloud[word] = { count: 0 };
      }
      //incriment word count
      wordCloud[word].count = wordCloud[word].count + 1;
      //check if this is the new maxCount
      maxCount =
        wordCloud[word].count > maxCount ? wordCloud[word].count : maxCount;
    });
  });
  Object.keys(wordCloud).forEach((word) => {
    wordCloud[word].fontWeight =
      (wordCloud[word].count > minCount
        ? (wordCloud[word].count / maxCount) * (maxFont - minFont) + minFont
        : minFont) + "px";
    wordCloud[word].color = colors[colorNumber];
    colorNumber = colorNumber > 4 ? 0 : colorNumber + 1;
  });

  return wordCloud;
};
const wordCloud = ref(createWordCloud(words));
</script>

<template>
  <div class="wordCloudContainer">
    <span
      v-for="(word, key) in wordCloud"
      :style="'font-size: ' + word.fontWeight + '; color: ' + word.color"
      >{{ key + " " }}
    </span>
  </div>
</template>

<style>
.wordCloudContainer {
  width: 1000px;
  height: 500px;
}
</style>
