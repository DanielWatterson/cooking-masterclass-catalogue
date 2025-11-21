<template>
  <div class="app">
    <header class="header">
      <div class="nav-bar">

        <!-- Left: Logo -->
        <div class="logo">🍳 CookMaster</div>

        <!-- Center: Title -->
        <h1 class="title">Cooking Workshop Catalogue</h1>

        <!-- Right: Wishlist -->
        <div class="wishlist">
          ❤️ Saved: <span>{{ wishlist.length }}</span>
        </div>

      </div>

      <!-- Filters row -->
      <div class="filters">
        <button 
          @click="showAvailableOnly = false" 
          :class="{ active: !showAvailableOnly }"
        >
          All Courses
        </button>

        <button 
          @click="showAvailableOnly = true" 
          :class="{ active: showAvailableOnly }"
        >
          Available Only
        </button>
      </div>
    </header>

    <!-- Catalogue Grid -->
    <main>
      <div class="courses-grid">
        <CourseCard
          v-for="course in filteredCourses"
          :key="course.title"
          :course="course"
          @add-to-wishlist="addToWishlist"
        />
      </div>
    </main>
  </div>
</template>

<script>
import CourseCard from "./components/CourseCard.vue";

export default {
  name: "App",
  components: { CourseCard },

  data() {
    return {
      showAvailableOnly: false,
      wishlist: [],

      courses: [
        {
          title: "Knife Skills",
          chef: "Chef Thor Ulrikson",
          price: "R250",
          level: "Beginner",
          available: true,
          image: "https://i.postimg.cc/NjgWTbTt/faw-chefs-knives.jpg",
        },
        {
          title: "Sauces & Seasoning",
          chef: "Chef Ben Fogel",
          price: "R300",
          level: "Intermediate",
          available: false,
          image: "https://i.postimg.cc/dVDn9vTP/istockphoto-1127973172.jpg",
        },
        {
          title: "Signature Dish",
          chef: "Chef Carla Garcia",
          price: "R400",
          level: "Advanced",
          available: true,
          image: "https://i.postimg.cc/4xnw1ZhR/2548301.jpg",
        },
        {
          title: "Bread Making",
          chef: "Chef David Parker",
          price: "R200",
          level: "Beginner",
          available: true,
          image: "https://i.postimg.cc/k4D8LrbN/r2-making-bread.jpg",
        },
        {
          title: "Cakes & Muffins",
          chef: "Chef Eva Von Der Heide",
          price: "R220",
          level: "Beginner",
          available: false,
          image: "https://i.postimg.cc/wTtzMwX8/20230302.jpg",
        },
        {
          title: "Decorating",
          chef: "Chef Fiona Gallagher",
          price: "R250",
          level: "Intermediate",
          available: true,
          image: "https://i.postimg.cc/MpKy1jGk/close-female-baker.jpg",
        },
      ],
    };
  },

  computed: {
    filteredCourses() {
      return this.showAvailableOnly
        ? this.courses.filter((c) => c.available)
        : this.courses;
    },
  },

methods: {
  addToWishlist(course) {
    const index = this.wishlist.findIndex(item => item.title === course.title);
    if (index === -1) {
      // Not in wishlist yet → add it
      this.wishlist.push(course);
    } else {
      // Already in wishlist → remove it
      this.wishlist.splice(index, 1);
      }
    },
  },
};
</script>

<style>

body {
  margin: 0;
  font-family: "Poppins", sans-serif;
  background: linear-gradient(to bottom, #fffaf0, #ffe6e1);
}

.app {
  max-width: 1300px;
  margin: auto;
  padding: 20px;
}

.header {
  background: linear-gradient(90deg, #ff7e5f, #feb47b);
  padding: 20px;
  border-radius: 12px;
  color: white;
  box-shadow: 0 4px 12px rgba(0,0,0,0.15);
  margin-bottom: 35px;
}

.nav-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
}

.logo {
  font-size: 1.7rem;
  font-weight: 700;
}

.title {
  font-size: 1.5rem;
  text-align: center;
  flex: 1;
  margin: 10px 0;
  font-weight: 600;
}

.wishlist {
  font-weight: bold;
  font-size: 1.2rem;
}

.filters {
  margin-top: 15px;
  display: flex;
  gap: 12px;
  justify-content: center;
}

.filters button {
  padding: 8px 18px;
  border-radius: 20px;
  border: none;
  cursor: pointer;
  font-weight: 600;
  background: white;
  color: #ff6347;
  transition: 0.25s ease;
}

.filters button.active {
  background: #ff4500;
  color: white;
}

.filters button:hover {
  transform: translateY(-2px);
}

.courses-grid {
  display: grid;
  gap: 25px;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  padding-bottom: 50px;
}
</style>
