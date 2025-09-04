<script>
export default {
  data() {
    return {
      posts: [],

    }
  },
  mounted() {
    this.posts = JSON.parse(localStorage.getItem("posts"))
    if (this.posts === null)
    {
      this.posts = []

      this.addPost("Солнышко", "1.jpg")
      this.addPost("Рыбки", "2.jpg")
      this.addPost("Крош уже не тот", "3.jpg")
      this.addPost("Гусеничка", "4.jpg")
      this.addPost("Улитка", "5.jpg")
    }
  },
  methods: {
    addPost(name, img)
    {
      let new_post = {}
      new_post.id = this.posts.length
      new_post.name = name
      new_post.img = img
      new_post.voices = 0
      new_post.current_voiced = false
      this.posts.push(new_post)
      this.savePosts()
    },
    savePosts()
    {
      localStorage.setItem("posts", JSON.stringify(this.posts))
    },
    voiceForPost(post_id)
    {
      for (let i = 0; i < this.posts.length; i++)
      {
        if (this.posts[i].id == post_id)
        {
            this.posts[i].voices += 1
            document.querySelector("#thank"+post_id).classList.add("visible")
            break
          }
      }
      this.posts.sort((a, b) => b.voices - a.voices)
      this.savePosts()
    },
  }
}
</script>

<template>
<h1>
  Голосование за лучшая подделку
</h1>
<div class="posts">
  <div class="post-block" v-for="post in posts">
    <img :src="post.img" alt="">
    <p>{{ post.name }}</p>
    <span>Голоса: {{ post.voices }}</span>
    <br>
    <button @click="voiceForPost(post.id)" v-if="post.current_voiced" class="liked">
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" class="bi bi-arrow-through-heart-fill" viewBox="0 0 16 16">
        <path fill-rule="evenodd" d="M2.854 15.854A.5.5 0 0 1 2 15.5V14H.5a.5.5 0 0 1-.354-.854l1.5-1.5A.5.5 0 0 1 2 11.5h1.793l3.103-3.104a.5.5 0 1 1 .708.708L4.5 12.207V14a.5.5 0 0 1-.146.354l-1.5 1.5ZM16 3.5a.5.5 0 0 1-.854.354L14 2.707l-1.006 1.006c.236.248.44.531.6.845.562 1.096.585 2.517-.213 4.092-.793 1.563-2.395 3.288-5.105 5.08L8 13.912l-.276-.182A23.825 23.825 0 0 1 5.8 12.323L8.31 9.81a1.5 1.5 0 0 0-2.122-2.122L3.657 10.22a8.827 8.827 0 0 1-1.039-1.57c-.798-1.576-.775-2.997-.213-4.093C3.426 2.565 6.18 1.809 8 3.233c1.25-.98 2.944-.928 4.212-.152L13.292 2 12.147.854A.5.5 0 0 1 12.5 0h3a.5.5 0 0 1 .5.5v3Z"/>
      </svg>
    </button>
    <button @click="voiceForPost(post.id)" v-else >
      <svg  xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" class="bi bi-arrow-through-heart" viewBox="0 0 16 16">
        <path fill-rule="evenodd" d="M2.854 15.854A.5.5 0 0 1 2 15.5V14H.5a.5.5 0 0 1-.354-.854l1.5-1.5A.5.5 0 0 1 2 11.5h1.793l.53-.53c-.771-.802-1.328-1.58-1.704-2.32-.798-1.575-.775-2.996-.213-4.092C3.426 2.565 6.18 1.809 8 3.233c1.25-.98 2.944-.928 4.212-.152L13.292 2 12.147.854A.5.5 0 0 1 12.5 0h3a.5.5 0 0 1 .5.5v3a.5.5 0 0 1-.854.354L14 2.707l-1.006 1.006c.236.248.44.531.6.845.562 1.096.585 2.517-.213 4.092-.793 1.563-2.395 3.288-5.105 5.08L8 13.912l-.276-.182a21.86 21.86 0 0 1-2.685-2.062l-.539.54V14a.5.5 0 0 1-.146.354l-1.5 1.5Zm2.893-4.894A20.419 20.419 0 0 0 8 12.71c2.456-1.666 3.827-3.207 4.489-4.512.679-1.34.607-2.42.215-3.185-.817-1.595-3.087-2.054-4.346-.761L8 4.62l-.358-.368c-1.259-1.293-3.53-.834-4.346.761-.392.766-.464 1.845.215 3.185.323.636.815 1.33 1.519 2.065l1.866-1.867a.5.5 0 1 1 .708.708L5.747 10.96Z"/>
      </svg>
    </button>
     <svg :id="`thank${post.id}`" class="thanks" width="200" height="100" viewBox="0 0 200 200">
            <rect x="10" y="10" width="180" height="180" rx="20" ry="20" fill="#FFD700" stroke="#FFA500" stroke-width="3"/>
            
            <circle cx="100" cy="80" r="40" fill="#FFCC99" stroke="#E6B88A" stroke-width="2"/>
        
            <circle cx="85" cy="75" r="5" fill="#333"/>
            <circle cx="115" cy="75" r="5" fill="#333"/>
            
            <path d="M85,95 Q100,110 115,95" fill="none" stroke="#333" stroke-width="2" stroke-linecap="round"/>
            
            <text x="100" y="150" font-family="Arial" font-size="20" text-anchor="middle" fill="#333">Спасибо!</text>
        </svg>
  </div> 
</div>
</template>

<style scoped>
@keyframes blankHide {
  from {
    opacity: 0.7;
  }
  to {
    opacity: 0;
    transform: translateX(30px) translateY(30px);
  }
}

.thanks {
  opacity: 0;
  position: absolute;
}
.thanks.visible {
  opacity: 0;
  animation-name: blankHide;
  animation-duration: 2s;
}

.posts {
  display: flex;
  flex-wrap: wrap;
  align-content: stretch;
  padding: 30px;
  align-items: baseline;
}

.post-block img{
  min-width: 20vw;
  max-width: 30vw;
  max-height: 50vh;
  border-radius: 30px;
}

.post-block {
  box-shadow: rgba(255,255,255,0.2) 8px  8px 18px 5px,
	            rgba(0,0,0,0.5)      -8px -8px 18px 5px;
  margin-right: 30px;
  margin-bottom: 30px;
  padding: 20px;
  border-radius: 30px;
}

.post-block button {
  border: none;
  background-color: lightgray;
  width: 46px;
  height: 46px;
  border-radius: 100%;
}

.liked {
  background-color: rgb(0, 119, 255);
}
</style>
