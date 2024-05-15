<!-- src/App.vue -->
<template>
  <div id="app">
    <header>
      <nav>
        <ul>
          <li><router-link to="/">Home</router-link></li>
          <li><router-link to="/update">Update</router-link></li>
        </ul>
      </nav>
    </header>
    <main>
      <router-view />
    </main>
  </div>
</template>

<script>
export default {
  name: 'App'
};
</script>

<style>
/* You can add global styles here */

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

header {
  background-color: #42b983;
  padding: 20px;
}

nav ul {
  list-style: none;
  padding: 0;
  margin: 10;
}

nav li {
  display: inline;
  margin-right: 20px;
}

nav a {
  color: white;
  text-decoration: none;
}

nav a.router-link-exact-active {
  font-weight: bold;
}

li{
  list-style-type: none;
}

footer {
  margin-top: 20px;
}

.input-container {
    gap: 10px;
  }
  .input-box {
    padding: 10px 15px;
    font-size: 16px;
    border: 2px solid #007BFF;
    border-radius: 5px;
    outline: none;
    transition: box-shadow 0.3s ease, border-color 0.3s ease;
    margin: 5px;
  }

  .add-btn {
    padding: 10px 20px;
    font-size: 16px;
    color: #fff;
    background-color: #007BFF;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.3s ease;
    margin: 10px;
  }

  .delete-btn {
    padding: 10px 20px;
    font-size: 16px;
    color: #fff;
    background-color: #ff2f00;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.3s ease;
    margin: 10px;
  }

  .back-btn {
    padding: 10px 20px;
    font-size: 16px;
    color: #fff;
    background-color: #1b604a;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.3s ease;
    margin: 10px;
  }

</style>
