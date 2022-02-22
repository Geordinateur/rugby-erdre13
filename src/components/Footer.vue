<script>
import { defineComponent } from "vue";
import { GoogleMap, Marker } from "vue3-google-map";

export default defineComponent({
  name: "Footer",
  components: {
    GoogleMap,
    Marker,
  },
  setup() {
    const center = { lat: 47.272482476303516, lng: -1.5166402888658894 };

    return { center };
  },
});
</script>

<template>
  <div class="footer">
    <div class="footer__google-maps">
      <GoogleMap
        api-key="AIzaSyC8xjG9MlqPYO8yWRduB8I44QucIrZFOqU"
        style="width: 100%; height: 500px"
        :center="center"
        :zoom="15"
      >
        <Marker :options="{ position: center }" />
      </GoogleMap>
    </div>
    <div class="footer__contact">
      <ol class="fa-ul">
        <li>
          <span class="fa-li"><i class="fas fa-phone-square-alt"></i></span>06
          18 70 60 38
        </li>
        <li>
          <span class="fa-li"><i class="fas fa-at"></i></span
          ><a href="mailto:asso.are13@gmail.com">asso.are13@gmail.com</a>
        </li>
        <li>
          <span class="fa-li"><i class="fab fa-facebook-square"></i></span
          ><a
            href="https://www.facebook.com/DragonsRugbyNantes/"
            target="_blank"
            >Les Dragons sont sur Facebook</a
          >
        </li>
        <li>
          <span class="fa-li"><i class="fas fa-map-marker-alt"></i></span
          >Gymnase Jean Jahan,<br />Rte de Saint-Joseph,<br />44300 Nantes
        </li>
      </ol>
    </div>
  </div>
</template>

<style lang="scss">
@import "../assets/scss/_mixins.scss";
@import "../assets/scss/_variables.scss";

.footer {
  padding: 5vh;
  @include large-only {
    padding: 10vh;
  }
  //margin-top: 10vh;
  background-color: grey;
  border-top: 0.7vh solid $grey-solid;
  display: flex;
  flex-flow: column;
  gap: 5vh;
  @include large-only {
    flex-flow: row;
  }
}
.footer__google-maps {
  flex: 3;
}
.footer__social {
  flex: 1;
  background-color: red;
}
.footer__contact {
  flex: 1;
  background-color: green;
  text-align: left;
}
.footer__contact__phone {
}
</style>
