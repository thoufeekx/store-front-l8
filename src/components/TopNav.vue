<template>
  <nav>
    <div class="logo">
      <a href="/">
        <img src="/best-buy-logo-2.png" alt="Algonquin Pet Store Logo">
      </a>
    </div>
    <button class="hamburger" @click="toggleNav">
      <span class="hamburger-icon"></span>
    </button>
    <ul class="nav-links" :class="{ 'nav-links--open': isNavOpen }">
      <li><router-link to="/" @click="closeNav">Products</router-link></li>
      <li><router-link to="/cart" @click="closeNav">Cart ({{ cartItemCount }})</router-link></li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'TopNav',
  props: ['cartItemCount'],
  data() {
    return {
      isNavOpen: false
    }
  },
  methods: {
    toggleNav() {
      this.isNavOpen = !this.isNavOpen
    },
    closeNav() {
      this.isNavOpen = false
    }
  }
}
</script>
<style scoped>
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #003f8e; /* Best Buy's blue color */
  color: #fff;
  padding: 0.5rem 2rem;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1); /* Soft shadow for depth */
}

nav img {
  width: 70px;
  height: auto;
  margin-right: 1rem;
}

.nav-links {
  display: flex;
  list-style: none;
  font-size: 1.2rem;
  font-weight: bold;
  gap: 2rem;
}

.nav-links li a {
  color: #ffffff;
  text-decoration: none;
  transition: color 0.3s ease;
}

.nav-links li a:hover {
  color: #ffcc00; /* Hover effect in yellow (Best Buy accent color) */
}

.hamburger {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0;
  margin: 0;
}

.hamburger-icon {
  display: block;
  width: 30px;
  height: 3px;
  background-color: #fff;
  position: relative;
  top: 50%;
  transform: translateY(-50%);
}

.hamburger-icon::before,
.hamburger-icon::after {
  content: '';
  display: block;
  width: 30px;
  height: 3px;
  background-color: #fff;
  position: absolute;
  left: 0;
}

.hamburger-icon::before {
  top: -8px;
}

.hamburger-icon::after {
  bottom: -8px;
}

@media (max-width: 768px) {
  .nav-links {
    display: none;
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    background-color: #003f8e;
    padding: 1rem;
    flex-direction: column;
    gap: 1rem;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  }

  .nav-links--open {
    display: flex;
  }

  .nav-links--open li a {
    font-size: 1.5rem;
  }

  .hamburger {
    display: block;
  }
}
</style>
