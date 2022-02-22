<script>
import Carousel from "../components/Carousel";
export default {
  name: 'Home',
  components: {
    Carousel
  }
}
</script>

<template>
  <div>
  <img class="logo__img" src="images/logo-dragons-sans-fonds.png" />
  <div class="article">
    <img class="img__left" src="images/stade-rugby-3.jpg" />
    <div class="left">
      <h2>Le club</h2>
      <h3>Qui sommes nous?</h3>
      <p>
        L’Association Rugby Erdre 13 est une association de loi 1901 et
        d’utilité publique dont l’objet est la pratique et la promotion du rugby
        à 13.
      </p>
      <p>
        L’association a été créée en 2015. Le club a pour volonté de fédérer les
        communes de l’Erdre autour d’une équipe nommée “Les Dragons de l’Erdre”
        dans une ambiance conviviale. Le club accueille tous les enfants de 4 à
        12 ans ainsi que leur parents.
      </p>
      <h3>Coordonnées</h3>
      <p>
        Pour tout renseignements, veuillez utiliser notre adresse e-mail
        asso.are13@gmail.com ou contacter Jennifer Sfartz au 06 18 70 60 38.
      </p>
    </div>
    <div class="right">
      <h2>Le Rugby à XIII c'est quoi ?</h2>
      <p>Alors qu’un match de rugby à 15 est interrompu par de nombreux arrêts de jeu, le rugby à 13 privilégie des remises en jeu rapides afin de réduire les temps morts. Ainsi, en supprimant les touches et les mêlées, le rugby à 13 se veut plus dynamique.</p>
      <table>
        <tr>
          <td></td>
          <td>rugby à 15</td>
          <td>rugby à 13</td>
        </tr>
        <tr>
          <td>durée d’un match</td>
          <td>80 min</td>
          <td>80 min</td>
        </tr>
        <tr>
          <td>temps de jeu effectif</td>
          <td>40 min</td>
          <td>70 min</td>
        </tr>
        <tr>
          <td>% de temps de jeu effectif</td>
          <td>50%</td>
          <td>88%</td>
        </tr>
      </table>
        <p>La différence fondamentale entre les deux sports réside dans la durée de possession du ballon par une équipe. Alors qu’au rugby à 15 la durée de possession est illimitée, le rugby à 13 n’autorise que 6 tentatives à une équipe pour inscrire un essai. Si elle échoue, elle doit rendre le ballon à son adversaire.</p>
        <p>Autre différence notable, le ballon ne peut pas être disputé à la suite d’un plaquage. Au rugby à 13, dès qu’un joueur est plaqué, on estime que son équipe a consommé une tentative. Le plaqueur relâche le plaqué, ce dernier se relève, il pose le ballon au sol, le fait rouler en arrière avec le pied puis une nouvelle action débute.</p>
    </div>
  </div>
  </div>
    <Carousel />
</template>

<style lang="scss">
@import "../assets/scss/_mixins.scss";

.left {
  text-align: left;
  flex: 1;
  width: 100%;
  background-color: green;
}
.img__left {
  @include large-only {
    width: 40vh;
  }
  width: 100%;
  box-shadow: $box-shadow-img;
}
.right {
  text-align: right;
  background-color: red;
  width: 100%;
}
</style>
