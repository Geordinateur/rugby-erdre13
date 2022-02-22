<script>
export default {
  name: 'Carousel',
  props: {
    msg: String
  }
}

class Carousel {
  /**
   *
   * @param {HTMLElement} element
   * @param {Object} options
   * @param {Object} [options.slidesToScroll=1] Nombre d'éléments à faire défiler
   * @param {Object} [options.slidesVisible=1] Nombre d'éléments visible dans un slide
   * @param {boolean} [options.loop=false] Dois-t-on boucler en fin de carousel
   */

  constructor(element, options = {}) {
    this.element = element;
    this.options = Object.assign(
      {},
      {
        slidesToScroll: 1,
        slidesVisible: 1,
        loop: false,
      },
      options
    );
    let children = [].slice.call(element.children);
    this.isMobile = false;
    this.currentItem = 0;
    this.moveCallbacks = [];

    // Modification du DOM
    this.root = this.createDivWithClass("carousel");
    this.container = this.createDivWithClass("carousel__container");
    this.root.setAttribute("tabindex", "0");
    this.root.appendChild(this.container);
    this.element.appendChild(this.root);
    this.items = children.map((child) => {
      let item = this.createDivWithClass("carousel__item");
      item.appendChild(child);
      this.container.appendChild(item);
      return item;
    });
    this.setStyle();
    this.createNavigation();

    // Évenements
    this.moveCallbacks.forEach((cb) => cb(0));
    this.onWindowResize();
    window.addEventListener("resize", this.onWindowResize.bind(this));
    this.root.addEventListener("keyup", (e) => {
      if (e.key === "ArrowRight") {
        this.next();
      } else if (e.key === "ArrowLeft") {
        this.prev();
      }
    });
  }

  /**
   *
   * Applique les bonnes dimesions aux éléments du carousel
   */
  setStyle() {
    let ratio = this.items.length / this.slidesVisible;
    this.container.style.width = (ratio * 100) + "%";
    this.items.forEach(
      (item) => (item.style.width = 100 / this.slidesVisible / ratio + "%")
    );
  }

  createNavigation() {
    let nextButton = this.createDivWithClass("carousel__next");
    let prevButton = this.createDivWithClass("carousel__prev");
    this.root.appendChild(nextButton);
    this.root.appendChild(prevButton);
    nextButton.addEventListener("click", this.next.bind(this));
    prevButton.addEventListener("click", this.prev.bind(this));
    if (this.options.loop === true) {
      return;
    }
    this.onMove((index) => {
      if (index === 0) {
        prevButton.classList.add("carousel__prev--hidden");
      } else {
        prevButton.classList.remove("carousel__prev--hidden");
      }
      if (this.items[this.currentItem + this.slidesVisible] === undefined) {
        nextButton.classList.add("carousel__next--hidden");
      } else {
        nextButton.classList.remove("carousel__next--hidden");
      }
    });
  }

  next() {
    this.gotoItem(this.currentItem + this.slidesToScroll);
  }

  prev() {
    this.gotoItem(this.currentItem - this.slidesToScroll);
  }

  /**
   * Déplace le carousel vers l'élément ciblé
   * @param {number} index
   */
  gotoItem(index) {
    if (index < 0) {
      if (this.options.loop) {
        index = this.items.length - this.slidesVisible;
      } else {
        return;
      }
    } else if (
      index >= this.items.length ||
      (this.items[this.currentItem + this.slidesVisible] ===
        undefined &&
        index > this.currentItem)
    ) {
      if (this.options.loop) {
        index = 0;
      } else {
        return;
      }
    }
    let translateX = (index * -100) / this.items.length;
    this.container.style.transform = "translate3d(" + translateX + "%, 0, 0)";
    this.currentItem = index;
    this.moveCallbacks.forEach((cb) => cb(index));
  }

  /**
   * @param {moveCallback} cb
   */
  onMove(cb) {
    this.moveCallbacks.push(cb);
  }

  onWindowResize() {
    let mobile = window.innerWidth < 800;
    if (mobile !== this.isMobile) {
      this.isMobile = mobile;
      this.setStyle();
      this.moveCallbacks.forEach((cb) => cb(this.currentItem));
    }
  }

  /**
   *
   * @param {string} className
   * @returns {HTMLElement}
   */

  createDivWithClass(className) {
    let div = document.createElement("div");
    div.setAttribute("class", className);
    return div;
  }

  /**
   *
   * @return {number}
   */
  get slidesToScroll() {
    return this.isMobile ? 1 : this.options.slidesToScroll;
  }

  get slidesVisible() {
    return this.isMobile ? 1 : this.options.slidesVisible;
  }
}

document.addEventListener("DOMContentLoaded", function () {
  /*
  new Carousel(document.querySelector("#carousel1"), {
    slidesVisible: 3,
    slidesToScroll: 2,
    loop: true,
  });

  new Carousel(document.querySelector("#carousel2"), {
    slidesVisible: 2,
    slidesToScroll: 2,
  });
  */
  new Carousel(document.querySelector("#carousel3"), {});
});
</script>

<template>
    <div class="container">
      <div id="carousel3">
        <div class="item">
          <div class="item__image">
            <img src="images/stade-rugby-3.jpg">
          </div>
          <div class="item__body">
            <h3>Titre de l'image</h3>
            <p>Description de l'image</p>
          </div>
        </div>
        <div class="item">
          <div class="item__image">
            <img src="images/stade-rugby-3.jpg">
          </div>
          <div class="item__body">
            <h3>Titre de l'image</h3>
            <p>Description de l'image</p>
          </div>
        </div>
        <div class="item">
          <div class="item__image">
            <img src="images/stade-rugby-3.jpg">
          </div>
          <div class="item__body">
            <h3>Titre de l'image</h3>
            <p>Description de l'image</p>
          </div>
        </div>
      </div>
    </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
@import "../assets/scss/_variables.scss";
@import "../assets/scss/_mixins.scss";

.container {
	display: flex;
	flex-flow: row nowrap;
	justify-content: center;
	align-items: center;
  //background-color: lightblue;
	//width: 100%;
  width: auto;
  padding: 4vh; 
  @include large-only {
    padding: 10vh;
  }
}

.title {
	font-size: 250px;
	color: #FFF;
	font-weight: bold;
	margin-bottom: 25px;
}

.item {
	background-color: #fff;
	//box-shadow: 0 15px 35px #3232321a,0 5px 15px #0000001a;
	transition: transform 0.3s filter 0.3s;
	transform: translate3d(0, -1px, 0);
}
.item:hover {
//	transform: translate3d(0, -10px, 0);
}

.item img {
	display: block;
	width: 100%;
	height: auto;
	object-fit: cover;
}
.item__image {
	padding: 0;
	margin: 0;
	//height: 400px;
  @include large-only {
    height: 80%;
  }
	margin-bottom: -200px;
}

.item__body {
  @include large-only {
    position: relative;
  }
	background-color: #FFFFFF;
	padding: 25px;
}

.item__title {
	font-size: 240px;
	margin-bottom: 5px;
	font-weight: bold;
	color: #232323;
}
.item__description {
	color: #585858;
}

.items {
	position: relative;
}

/* img {
	width: auto !important;
	width: 100%;
	max-width: 678px;
	float: left;
	clear: both;
	padding-bottom: 10px;
}*/


/**
 * Carousel
 */

 #carousel3 {
  width: 100%;
 }
	.carousel {
		position: relative;
		overflow: hidden;
		box-shadow: $box-shadow;
	}

	.carousel__container {
		transition: transform 0.3s;
		transform: translate3d(0, 0, 0)
	}
	.carousel__container::after {
		content: '';
		clear: both;
		display: table;
	}

	.carousel__item {
		float: left;
	}

	.carousel__next, .carousel__prev {
		position: absolute;
		width: 40px;
		height: 40px;
		background: #FFF url(../assets/right.svg) center center no-repeat;
		background-size: 20px 20px;
		border-radius: 50%;
		top: 50%;
		margin-top: -20px;
		right: +20px;
		box-shadow: 0 15px 35px #3232321a,0 5px 15px #0000001a;
		cursor: pointer;
		transition: transform 0.3s, opacity 0.3s;
	}
	.carousel__next:hover, .carousel__prev:hover {
		transform: scale(1.2)
	}
	.carousel__prev {
		background-image: url(../assets/left.svg);
		right: auto;
		left: +20px;
	}
	.carousel__next--hidden,.carousel__prev--hidden  {
		opacity: 0;
	}
</style>
