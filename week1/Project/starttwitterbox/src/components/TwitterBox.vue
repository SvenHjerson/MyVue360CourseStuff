<template>
  <div>
    <h1>Project Twitter Box Client</h1>

    <div class="box">
      <form action>
        <textarea
          v-model.trim="newTweet"
          @input="checkLength"
          type="text"
          placeholder="Tweet Something Awesome"
        />
        <button @click.prevent="tweetMessage">Submit</button>
        <p>Charachters remaining {{ maxLength - tweetLength }}</p>
      </form>
    </div>
    <div v-if="tweets.length > 0">
      <h2>Tweets</h2>
      <div v-for="tweet in tweets" :key="tweet.id">
        <div>
          <h3>Tweet #{{ tweet.id }}</h3>
        </div>
        <div>
          <p>{{ tweet.message }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TwitterBox",
  data() {
    return {
      newTweet: "",
      maxLength: 280,
      tweetLength: 0,
      tweets: []
    }
  },
  methods: {
    tweetMessage() {
      let tweetDetails = {
        id: this.tweets.length + 1,
        timestamp: Date.now(),
        message: this.newTweet
      }
      this.tweets.push(tweetDetails)
      this.newTweet = ""
      this.tweetLength = 0
    },
    checkLength(event) {
      if (event.target.value.length > this.maxLength) {
        this.newTweet = this.newTweet.substr(0, this.maxLength)
        this.tweetLength = this.maxLength
      } else {
        this.tweetLength = event.target.value.length
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.box {
  width: 33%;
  background-color: #b8dcdc;
  height: auto;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1),
    0 10px 10px -5px rgba(0, 0, 0, 0.04);
}
button {
  margin-left: 10px;

}
</style>