<script>
import NavLink from "./components/NavLink";
import Footer from "./components/Footer";

export default {
  name: "app",
  components: {
    NavLink,
    Footer,
  },
  mounted() {
    // When the user scrolls the page, execute myFunction
    window.onscroll = function () {
      myFunction();
    };

    // Get the navbar
    var navbar = document.getElementById("navbar");

    // Get the offset position of the navbar
    //var sticky = navbar.offsetTop - 370;
    var sticky = navbar.offsetTop;

    // Add the sticky class to the navbar when you reach its scroll position. Remove "sticky" when you leave the scroll position
    function myFunction() {
      if (window.pageYOffset >= sticky) {
        navbar.classList.add("sticky");
        navbar.classList.add("sticky__remove");
        navbar.classList.remove("enable");
      } else {
        navbar.classList.remove("sticky");
        navbar.classList.add("enable");
      }
    }
  },
};
</script>

<template>
  <div id="navbar" class="navbar">
    <NavLink url="/" icon="fas fa-home" text="Accueil" />
    <!--<NavLink url="/about" icon="fas fa-football-ball" text="Le club" />-->
    <NavLink url="/contact" icon="fas fa-envelope-open-text" text="Nous contacter" />
    <NavLink url="/registration" icon="fas fa-user-plus" text="Inscription" />
    <NavLink url="/calendar" icon="fas fa-calendar-alt" text="Calendrier" />
  </div>
  <div id="main" class="content">
    <router-view />
  </div>
  <Footer />
</template>

<style lang="scss">
@import "../src/assets/scss/_variables.scss";
@import "../src/assets/scss/_mixins.scss";

html {
}
body {
  padding: 0;
  margin: 0;
  transition: 0.3s;
  //background-image: url("../public/images/grass-vector-top.png");
  //background-repeat: repeat-x;
  background-image: linear-gradient(
    -45deg,
    transparent 25%,
    rgb(144, 164, 174, 0.2) 25%,
    rgb(144, 164, 174, 0.2) 50%,
    transparent 50%,
    transparent 75%,
    rgb(144, 164, 174, 0.2) 75%,
    rgb(144, 164, 174, 0.2) 100%
  );
  background-size: 30px 30px;
  //animation: stripe 80s linear infinite;
  background-attachment: fixed;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  min-height: 100vh;
}

/* Style the navbar */
.navbar {
  overflow: hidden;
  margin-top: 50px;
  padding-top: 20px;
  //background-color: red;
  z-index: 1;
  &.enable {
    //transition: 0.35s all ease-in-out;
  }
}

.navbar__link {
  //overflow: hidden;
  display: inline-block;
  transform: translateY(-2px);
  background: none;
  color: $black;
  position: relative;
  font-size: 1.5em;
  font-weight: bold;
  padding: 0 10px;
  &:after {
    transition: all 0.3s;
    content: "";
    z-index: -1;
    border-radius: 10px;
    position: absolute;
    bottom: 2px;
    left: 0;
    right: 0;
    height: 10px;
    background-color: $blue3;
    width: 100%;
    opacity: 0;
  }
  &.router-link-exact-active:after {
    opacity: 1;
    background-color: $blue1;
  }
  &.router-link-exact-active:hover:after {
    background-color: $blue3;
  }
  &:hover:after {
    opacity: 1;
  }
  & > span {
    display: none;
    @include large-only {
      display: inline-block;
    }
  }
}
.logo {
}
.logo__img {
  filter: $drop-shadow;
  max-width: 740px;
  width: 100%;
  margin: 5vh 0;
}

/* Page content */
.content {
  padding: 30px 0;
}

/* The sticky class is added to the navbar with JS when it reaches its scroll position */
.sticky {
  position: fixed;
  top: 0;
  width: 100%;
  background-color: $white;
  padding: 20px 0;
  margin: 0;
  box-shadow: $box-shadow;
  //transition: 0.1s all ease-out;
}

.sticky__remove:before {
  & > body {
    content: "HELLO WORLD";
  }
}

/* Add some top padding to the page content to prevent sudden quick movement (as the navigation bar gets a new position at the top of the page (position:fixed and top:0) */
.sticky + .content {
  //padding-top: 9.3vh;
  padding-top: 129px;
}

.article {
  //  background: linear-gradient(
  //    to bottom,
  //    transparent,
  //    white 50px,
  //    white,
  //    transparent
  //  );
  background-color: $white;
  display: flex;
  flex-flow: column;
  justify-content: center;
  padding: 6vh 4vh;
  border-top: 0.7vh solid $grey-transparent;
  border-bottom: 0.7vh solid $grey-transparent;
  margin-top: 10vh;
  @include large-only {
    padding: 6vh 10vh;
    flex-flow: row wrap;
    gap: 3vh;
  }
}

h2 {
  order: -1;
  width: 100%;
}

.icon {
  font-size: 5vh;
  color: $grey-solid;
}

@keyframes stripe {
  0% {
    background-position: 0 0;
  }
  100% {
    background-position: 100% 0;
  }
}
</style>
