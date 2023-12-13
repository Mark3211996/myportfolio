<template>
  <div @click="closeNavBar">
    <header class="header">
      <div class="react-icon" @click="toggleNavBar" style="cursor: pointer">
        <i class="iconBar" v-if="!navBar" @click.stop="toggleNavBar">Menu</i>
        <i class="iconBar" v-else @click.stop="toggleNavBar">Back</i>
      </div>
      <nav
        class="navbar"
        :style="{
          width: navBar ? '200px' : '',
          padding: navBar ? '10px 20px 0px 0px' : '0',
        }"
      >
        <a href="#" style="--i: 1" class="active">Home</a>
        <a href="#about" style="--i: 2">About</a>
        <a href="#skills" style="--i: 3">Skill</a>
        <a href="#todo-list" style="--i: 3">Todo</a>
        <a href="#contact" style="--i: 5">Contact</a>
        
      </nav>
    </header>

    <section class="home">
      <div class="home-content">
        <h3>Hello!! im</h3>
        <h1>Mark Louie Abaca</h1>
        <h3>BSIT student</h3>
        
        <p>Web Designer</p>

        <div class="home-sci">
          <a
            href="https://web.facebook.com/profile.php?viewas=100000686899395&id=100052340933553"
          >
            <i class="bx bxl-facebook"></i>
          </a>
          <a
            href="https://www.instagram.com"
            :style="{ '--i': 8 }"
          
          >
            <i class="bx bxl-instagram"></i>
          </a>
          <a
            href="https://github.com/Mark3211996"
            target="_blank"    
          >
            <i class="bx bxl-github"></i>
          </a>
          <a
            href=""
            :style="{ '--i': 10 }"
          >
            <i class="bx bxl-tiktok"></i>
          </a>
        </div>
      </div>
      <div class="images">
        <img src="../assets/images/newme.jpg" alt="">
      </div>
    
    </section>

    <section class="about" id="about">
      <div class="about-img">
     
      </div>
      <div class="about-info">
        <h2>About <span>Me</span></h2>
        <br>
        <h4>Who I Am</h4>
        <p>
         I am Mark Louie Abaca,a 27 years old and a 4th year bsit student!, im a silent boy
         and always motivated, i love to research something that is unexplainable matter
         and im not a pro in coding, but it comes
         in styling and planning that is my field.
        </p>
        
      </div>
    </section>

    <section style="display: flex; height: 100vh">
      <div class="container1" id="skills">
        <h1 class="heading1">My <span style="color: #0ef">Skills</span></h1>
        <div class="technical-bars">
          <div v-for="(skill, index) in skills" :key="index" class="bar">
            <i :class="skill.iconClass" :style="{ color: skill.color }"></i>
            <div class="info">
              <span>{{ skill.name }}</span>
            </div>
            <div :class="['progress-line', skill.class]">
              <span></span>
            </div>
          </div>
        </div>
      </div>

    </section>
    <section id="todo-list">
      <div class="todo-container">
        <div class="todo-body">
          <h1>Todo List App</h1>
          <div class="input-list">
            <div class="search-list">
              <input
                type="text"
                v-model="searchText"
                placeholder="Search Todo..."
              />
              <i class="bx bx-search-alt-2"></i>
            </div>
          </div>
          <div v-for="(todo, index) in todos" :key="index" class="todo-list">
            <p :class="{ completed: todo.completed }">{{ todo.text }}</p>
            <!-- <div> -->
            <i @click="toggleCompletionStatus(index)" class="bx bx-check"></i>
            <i
              @click="removeTodo(index)"
              class="bx bx-x"
              v-if="!todo.completed"
            ></i>
            <!-- </div> -->
          </div>
          <div class="clear-all"><button @click="clearAll" v-if="incompleteTodosExist">Clear All</button></div>

          <div class="add-todo">
            <h1>Add New List</h1>
            <div class="new-input">
              <input
                type="text"
                v-model="newTodo"
                placeholder="Write Here..."
              />
              <i @click="addTodo" class="bx bx-plus"></i>
            </div>
          </div>
        </div>
      </div>
    </section>

      <div class="contact-form" id="contact">
       <form action="/">
            <div class="title">
              <h2>Contact me</h2>
            </div>
            <div>
              <input class="fname" type="text" name="name" placeholder="Full name">
              <input type="text" name="name" placeholder="Email">
              <input type="text" name="name" placeholder="Phone number">
              <input class="textarea" name="text" placeholder="Suggestion" id="">
            </div>
            <button class="btn">Submit</button>
          </form>
     </div>
  

    

    <div>
      <div class="last-text">
        <p>copy right ~~ year 2023</p>
      </div>
    </div>
  </div>
  
</template>

<style>
.completed {
  text-decoration: line-through; 
  text-align: center; 
}
</style>

<script>
import "../assets/css/Style.css";

// boxicons
import "boxicons/css/boxicons.min.css";

export default {
  data() {
    return {
      navBar: false,
      searchText: "",
      newTodo: "",
      todos: [
        {
          text: "sample!",
        },
        {
          text: "sample2",
        },
        { text: "sample3" },
      ],
      skills: [
        {
          name: "HTML",
          iconClass: "bx bxl-html5",
          color: "#c95d2e",
          class: "html",
        },
        {
          name: "CSS",
          iconClass: "bx bxl-css3",
          color: "#147bbc",
          class: "css",
        },
        {
          name: "Java",
          iconClass: "bx bxl-java",
          color: "#b0bc1e",
          class: "javascript",
        },
      ],
    };
  },
  computed: {
    incompleteTodosExist() {
      return this.todos.some((todo) => !todo.completed || todo.completed);
    },
  },
  methods: {
    toggleNavBar() {
      this.navBar = !this.navBar;
    },
    closeNavBar() {
      this.navBar = false;
    },
    submitForm() {
      // Handle form submission here
    },
    addTodo() {
      if (this.newTodo.trim() !== "") {
        this.todos.push({ text: this.newTodo });
        this.newTodo = "";
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },

    toggleCompletionStatus(index) {
      this.todos[index].completed = !this.todos[index].completed;
    },

    clearAll() {
      this.todos = this.todos.filter(
        (todo) => !todo.completed && todo.completed
      );
    },
  },
};
</script>