<template>
  <div class="container">
    <h1>Wanted Poster Workshop</h1>
    <p>Become the Outlaw!</p>
    <div class="inputs">
      <input type="file" @change="onFileChange" class="file-input" />
      <div v-if="isImageUrlExist()">
        <label for="bounty">Bounty : </label>
        <input
          id="bounty"
          v-model="bounty"
          placeholder="Bounty"
          class="input-field"
        />
      </div>
      <div v-if="isImageUrlExist()">
        <label for="crime"> Crime : </label>
        <input
          id="crime"
          v-model="crime"
          placeholder="Crime"
          class="input-field"
        />
      </div>
    </div>
    <div class="wanted-poster-container">
      <div class="wanted-poster">
        <div class="image-wrapper">
          <img
            v-if="imageUrl"
            :src="imageUrl"
            class="fitted-image"
            alt="Wanted Poster"
          />
        </div>
        <div v-if="isImageUrlExist()" class="poster-details">
          <div class="poster-details-crime">{{ crime }}</div>
          <div class="poster-details-bounty">${{ bounty }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      imageUrl: "",
      name: "",
      bounty: "",
      crime: "",
    };
  },
  mounted() {
    // Ensure the adsbygoogle array is present
    window.adsbygoogle = window.adsbygoogle || [];
    // Push a new adsbygoogle request
    window.adsbygoogle.push({});
  },
  methods: {
    onFileChange(e) {
      const file = e.target.files[0];
      this.imageUrl = URL.createObjectURL(file);
      this.name = "";
      this.bounty = this.generateRandomBounty();
      this.crime = this.generateRandomCrime();
    },
    isImageUrlExist() {
      return !(this.imageUrl == null || this.imageUrl === "");
    },
    generateRandomBounty() {
      const minBounty = 1;
      const maxBounty = 100000;
      const bounty =
        Math.floor(Math.random() * (maxBounty - minBounty) + 1) + minBounty;
      return bounty;
    },
    generateRandomCrime() {
      const crimes = [
        "Gaining weight",
        "Stealing my heart",
        "Not dieting this year",
        "Skipping morning coffee",
        "Oversleeping",
        "random cirme 1",
        "random cirme 2",
        "Waking up late on the weekend",
        "Doodling",
        "Regretting after eating chicken",
      ];

      const crime = crimes[Math.floor(Math.random() * crimes.length)];
      return crime;
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Notable&display=swap");
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

.inputs {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  margin-bottom: 20px;
}

.file-input {
  padding: 10px;
  font-size: 12px;
}

.input-field {
  width: 200px;
  padding: 5px;
  font-size: 12px;
  border: 1px solid #8b0f2e;
  box-sizing: border-box;
}

.wanted-poster-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.wanted-poster {
  position: relative;
  width: 325px;
  height: 431px;
  padding: 5px;
  background: url("../assets/wanted_poster.jpg");
  background-size: cover;
  text-align: center;
  color: #2e1b0d;
  font-family: "Old Western", serif;
}

.poster-text {
  font-size: 60px;
  font-weight: bold;
  margin-bottom: 5px;
  text-shadow: 2px 2px 4px #000;
}

.poster-details {
  margin-top: 20px;
  text-align: center;
  font-family: "Notable", sans-serif;
  font-weight: 400;
  font-style: normal;
}
.poster-details-bounty {
  position: absolute;
  top: 360px; /* 위에서 50px 아래 */
  left: 50%;
  transform: translateX(-50%);
  margin-top: 2px;
  font-size: 25px;
  font-weight: bold;
}
.poster-details-crime {
  position: absolute;
  top: 329px; /* 위에서 50px 아래 */
  left: 50%;
  transform: translateX(-50%);
  font-size: 18px;
  font-weight: bold;
  white-space: nowrap; /* 텍스트가 한 줄에 유지되도록 함 */
}

.image-wrapper {
  position: absolute;
  left: 12px;
  top: 78px;
  right: 13px;
  bottom: 123px;
  overflow: hidden;
}

.fitted-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;

  filter: sepia(0.35) saturate(1) hue-rotate(-10deg);
}
</style>
