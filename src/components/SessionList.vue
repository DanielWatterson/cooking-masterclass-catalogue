<template>
  <div class="sessions">
    <h3>Workshop Sessions</h3>
    <ul class="sessions-container">
      <li 
        v-for="(session, index) in sessions" 
        :key="index"
        :class="{ active: session.title === activeSession }"
      >
        <img :src="session.image" :alt="session.title" class="session-image" />
        <strong>{{ session.title }}</strong>
        <p>{{ session.desc }}</p>
        <button @click="bookSession(session.title)">Book Now</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "SessionList",
  props: {
    sessions: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      activeSession: null
    };
  },
  methods: {
    bookSession(title) {
      this.activeSession = title;
      alert(`You booked: ${title}`);
    }
  }
};
</script>

<style scoped>
.sessions ul {
  padding: 0;
  list-style: none;
}

.sessions li {
  background: #ffffff;
  padding: 15px;
  border-radius: 10px;
  margin-bottom: 10px;
  box-shadow: 0 1px 4px rgba(0,0,0,0.1);
}

.session-image {
  width: 100%;
  max-height: 200px;
  object-fit: cover;
  border-radius: 10px;
  margin-bottom: 10px;
}

button {
  background: #ff6347;
  color: white;
  padding: 8px 15px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
button:hover {
  background: #ff4500;
}

.active {
  border: 2px solid #ff6347;
  background: #fff3f0;
}
</style>
