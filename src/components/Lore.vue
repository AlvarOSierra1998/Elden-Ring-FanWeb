
    <!--ANTIGUO CODIGO-->
    <!---<nav class="lore">
        <!----<img  src="../assets/goldenorderlogo.png" alt="golden-order-logo">---
        <div class="container">

            <div class="buttons-container">
                <div class="box-button box-button-lore">
                    <button @click="mostrarLoreDesc"></button>
                </div>
                <div class="loreabsolute">
                    <a href="#lore">Lore</a>
                </div>

                <div class="box-button box-button-npcs">
                    <button @click="mostrarLorePersonajes"><a href="#characters">Characters</a></button>
                </div>

                <div class="box-button box-button-trailer">
                    <button><a href="#gameplay">trailer</a></button>
                </div>

                <div class="box-button box-button-gallery">
                    <button><a href="#gallery">Gallery</a></button>
                </div>
            </div>
        </div>
    </nav>
    <!--LORE--
    <section class="color">
        <div class="container-dsc" v-if="mostrarLore" :class="{ desc: mostrarLoreDesc }">
            <div class="desc">
                <img class="book" src="../assets/ER_Icon_Book_Golden_Order_Principia.webp" alt="">
                <p id="lore">L a Historia de Shadows of the erdtree va más allá de las Tierras Intermedias, esta nueva
                    aventura tiene lugar en el Reino de las sombras, donde el Empíreo Miquella se encuentra.
                    Tras nuestra lucha frente al <a @click="mostrarLoreMogh" href="#mohg">Señor de la Sangre Mohg</a> y
                    habiendo derrotado tambien al semidios <a href="#radhan">Radhan Azote de las estrellas</a>. Debemos
                    acudir al Panteon dinástico.
                    donde la crisálida de un dios dormido se encuentra.
                    Allí nos encontraremos con la <a href="#leda"> Caballera de la aguja Leda</a>, quien nos dará la
                    bienvenida a este nuevo mundo, <a href="#sombras">El Reino de las Sombras</a>.
                    <br>
                    <br id="lore">
                    Tras hablar con Leda nos explica que ella también fue guiada por la fe al igual que sus compatriotas
                    quienes han acudido a la llamada de Miquella el Cortés, Leda nos señala a la crisalida del empiero
                    para asi poder transportarnos a las tierras sombrías.
                    <br>
                    <br>
                    Una vez en el reino de las sombras, nos encontramos con un mundo oscuro y desolado, donde la luz no
                    existe y la oscuridad reina, en este mundo nos encontramos con seres de pesadilla y criaturas que no
                    pertenecen a este mundo.
                    <br>
                </p>



            </div>

            
            



        </div>
    </section>-->
    <!---PERSONAJES --
    <div v-if="mostrarPersonajes" :class="{ desc: mostrarLorePersonajes }">
            <div>
                <button> Dioses /</button>
                <button id="characters"  class="btn-semi" @click="mostrarDescSemidioses"><a href="#Semidioses"> Semidioses </a>  / </button>
                <button >Npcs </button>
            </div>
    </div>

    <!---NPCS  --
   
    <section class="color">
            <div>
                <div class="container-dsc" v-if="semidioses" :class="{ desc: mostrarDescSemidioses }">

                    <div class="desc">
                        <img class="book" src="../assets/Mohg.webp" alt="">

                        <p class="lore-desc" id="Semidioses">Mohg, el Señor de la Sangre, era el hermano gemelo de Morgott,
                            ambos nacidos del Linaje
                            Dorado y malditos como Augurios. Mientras que Morgott rechazó su maldición, Mohg la abrazó y
                            en
                            las profundidades subterráneas se conectó con la Madre Informe, un dios exterior que le
                            otorgó
                            poderosas habilidades de hemofuego. Tras la destrucción del Círculo de Elden, Mohg escapó y
                            reclamó un fragmento del Círculo roto, asumiendo el título de Señor de la Sangre y
                            comenzando a
                            reunir seguidores en su guarida subterránea.
                            <br>
                            <br>
                            Mohg desarrolló una obsesión con Miquella el Inmaculado, un Empíreo con el potencial de
                            convertirse en divinidad. Secuestró a Miquella de su Árbol Hierático, con la intención de
                            elevarlo a la divinidad y gobernar juntos como monarcas. Desde su Palacio de Mohgwyn, Mohg
                            estableció su dinastía, servido por nobles y seguidores que ofrecían sangre para despertar a
                            Miquella, aunque nunca logró obtener una respuesta del joven Empíreo.
                            <br>
                            <br>
                            Eventualmente, el Sinluz encontró el palacio de Mohg y lo enfrentó en combate. A pesar de
                            desatar todo el poder de su sangre maldita, Mohg fue derrotado. Tras su muerte, Miquella
                            intentó
                            usar el cuerpo de Mohg como recipiente para el alma del General Radahn, pero ambos fueron
                            derrotados por el Sinluz, y el cuerpo de Mohg fue destruido, sin dejar rastro.

                        </p>
                    </div>
                </div>
            </div>

        </section>


    -->

    <template>
  <div id="app" class="wrapper" v-cloak :class="{'is-previous': isPreviousSlide, 'first-load': isFirstLoad}">
    <div class="slide-wrapper" 
         v-for="(slide, index) in slides" 
         :class="{ active: index === currentSlide }"
         :style="{ 'z-index': (slides.length - index), 'background-image': 'url(' + slide.bgImg + ')' }">
      <div class="slide-inner">
        <div class="slide-bg-text">
          <p>{{ slide.headlineFirstLine }}</p>
          <p>{{ slide.headlineSecondLine }}</p>
        </div>
        <div class="slide-rect-filter">
          <div class="slide-rect" :style="{'border-image-source': 'url(' + slide.rectImg + ')'}"></div>
        </div>
        <div class="slide-content">
          <h1 class="slide-content-text">
            <p>{{ slide.headlineFirstLine }}</p>
            <p>{{ slide.headlineSecondLine }}</p>
          </h1>
          <!--CALL TO ACTION-->
          <a href="lore" @click.prevent="toogle()" class="slide-content-cta">Mostrar</a> 
        </div>
        <!--modal-->
              <Modal :show="mostrar" @close="toogle" :class="{ desc: mostrar }"  >
                  <bl>
                    <img src="../assets/ER_icon_Book_Golden_Order_Principia.webp" class="book animate__animated animate__fadeInLeft" alt="Golden Order Principia">
                      <p id="lore">
                          {{ description }}
                        </p>
                    </bl> 
                </Modal>

        <h2 class="slide-side-text">
          <span>{{ slide.sublineFirstLine }} / </span>
          <span>{{ slide.sublineSecondLine }}</span>
        </h2>
      </div>
    </div>
    <div class="controls-container">
      <button class="controls-button" 
              v-for="(slide, index) in slides"
              :class="{ active: index === currentSlide }"
              @click="updateSlide(index)">
        {{ slide.headlineFirstLine }} {{ slide.headlineSecondLine }}
      </button>
    </div>
    <div class="pagination-container">
      <span class="pagination-item"
            v-for="(slide, index) in slides"
            :class="{ active: index === currentSlide }"
            @click="updateSlide(index)">
      </span>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import Modal from './Modal.vue';

const mostrar = ref(false);
const toogle = () => {
    mostrar.value = !mostrar.value;
}
const currentSlide = ref(0);
const isPreviousSlide = ref(false);
const isFirstLoad = ref(true);
const slides = ref([
  {
    headlineFirstLine: "",
    headlineSecondLine: "Las Tierras de las sombras",
    sublineFirstLine: "Shadows of the erdtree",
    sublineSecondLine: "lore",
    bgImg: "https://images2.alphacoders.com/136/1363595.jpeg",
    rectImg: "https://images6.alphacoders.com/136/1366850.jpeg"
  },
  {
    headlineFirstLine: "Nulla",
    headlineSecondLine: "Auctor",
    sublineFirstLine: "Il n'y a rien de neuf sous",
    sublineSecondLine: "le soleil",
    bgImg: "https://i.postimg.cc/Qx34VNXM/slide1.jpg",
    rectImg: "https://i.postimg.cc/ryWZ8R2b/slide-rect1.jpg"
  },
  {
    headlineFirstLine: "Nullam",
    headlineSecondLine: "Ultricies",
    sublineFirstLine: "Τίποτα καινούργιο κάτω από",
    sublineSecondLine: "τον ήλιο",
    bgImg: "https://i.postimg.cc/t4RBtrnQ/slide2.jpg",
    rectImg: "https://i.postimg.cc/3JFLGMRF/slide-rect2.jpg"
  }
]);

const updateSlide = (index) => {
  isPreviousSlide.value = index < currentSlide.value;
  currentSlide.value = index;
  isFirstLoad.value = false;
};

const fetchSlides = async () => {
        try {
          const response = await fetch('/data.json');
          if (!response.ok) {
            throw new Error('Network response was not ok');
          }
          const data = await response.json();
          slides.value = data;
        } catch (error) {
          console.error('Error fetching slides:', error);
        }
      };
      

onMounted(() => {
    //fetchSlides()
  const productRotatorSlide = document.getElementById("app");
  let startX = 0;
  let endX = 0;

  productRotatorSlide.addEventListener("touchstart", (event) => startX = event.touches[0].pageX);

  productRotatorSlide.addEventListener("touchmove", (event) => endX = event.touches[0].pageX);

  productRotatorSlide.addEventListener("touchend", () => {
    const threshold = startX - endX;

    if (threshold < 150 && currentSlide.value > 0) {
      currentSlide.value--;
    }
    if (threshold > -150 && currentSlide.value < slides.value.length - 1) {
      currentSlide.value++;
    }
  });
});

const description = `L a Historia de Shadows of the erdtree va más allá de las Tierras Intermedias, esta nueva
                    aventura tiene lugar en el Reino de las sombras, donde el Empíreo Miquella se encuentra.
                    Tras nuestra lucha frente al Señor de la Sangre Mohg y
                    habiendo derrotado tambien al semidios Radhan Azote de las estrellas. Debemos
                    acudir al Panteon dinástico
                    donde la crisálida de un dios dormido se encuentra.
                    Allí nos encontraremos con la  Caballera de la aguja Leda, quien nos dará la
                    bienvenida a este nuevo mundo, El Reino de las Sombras.
                    Tras hablar con Leda nos explica que ella también fue guiada por la fe al igual que sus compatriotas
                    quienes han acudido a la llamada de Miquella el Cortés, Leda nos señala a la crisalida del empiero
                    para asi poder transportarnos a las tierras sombrías.
                    Una vez en el reino de las sombras, nos encontramos con un mundo oscuro y desolado, donde la luz no
                    existe y la oscuridad reina, en este mundo nos encontramos con seres de pesadilla y criaturas que no
                    pertenecen a este mundo.`;
                  

// Mostrar Lore
// const mostrarLore = ref(false);
// const mostrarLoreDesc = () => {
//     mostrarLore.value = !mostrarLore.value;

// }

// //Mostrar Lore Personajes botones
// const mostrarPersonajes = ref(false);
// const mostrarLorePersonajes = () => {
//     mostrarPersonajes.value = !mostrarPersonajes.value;
// }


// const semidioses = ref(false);
// const mostrarDescSemidioses = () => {
//     semidioses.value = !semidioses.value;
// }

</script>



<style scoped>
@import url("./StyleComponents/loreDesc.css");
.book{
    width: 300px;
    position: absolute;
    top: 0;
    left: 0;
    margin: auto;
}


/*estilos antiguos
.loreabsolute{
    position: absolute;
    z-index: 999999999999999;
    left: 0;
    float: left;
    width: 31% !important;
    font-size: 3em !important;
    font-weight: 300;
}

/***GENERAL BOX *

.btn-semi{

    

    margin: auto !important;
    padding-bottom: 0 !important;
    padding-top: 90px !important;
    border-radius: 5px;


}

.btn-semi:hover {

    text-shadow: 0 0 30px #ebc20b;
    transition: 0.5s;
    color: aliceblue;
}


.box-button {

    background-color: rgba(44, 44, 44, 0.63);

    margin: auto !important;
    padding-bottom: 0 !important;
    padding-top: 370px !important;
    border-radius: 5px;


}

/************ *

.box-button-lore {
    background-image: url("../assets/fondo-mobil1.webp");
    background-size: cover;
    background-repeat: no-repeat;
    /* border-image: fill 0 linear-gradient(to top, rgba(0, 0, 0, 0.493), rgba(0, 0, 0, 0.5)); *
    transition: opacity 1s ease-in-out;
    position: relative;
    box-shadow: inset 0 0 0 1000px rgba(0, 0, 0, 0.5);
    box-shadow: 30px 30px 30px 30px rgba(0, 0, 0, 0.5);
    transition: 0.5s ease-in-out;
    transition: border-image 0.5s ease-in-out;
    border-radius: 5px;

}

.box-button-lore:hover {

    transition: 0.5s ease-in-out;
}

.box-button-npcs {
    background-image: url("../assets/leda.jpeg");
    background-size: cover;
    background-repeat: no-repeat;
    /* border-image: fill 0 linear-gradient(to top, rgba(0, 0, 0, 0.493), rgba(0, 0, 0, 0.5)); *
    transition: opacity 1s ease-in-out;
    position: relative;
    box-shadow: inset 0 0 0 1000px rgba(0, 0, 0, 0.5);
    box-shadow: 30px 30px 30px 30px rgba(0, 0, 0, 0.5);
    transition: 0.5s ease-in-out;
    transition: border-image 0.5s ease-in-out;
    border-radius: 5px;

}

.box-button-trailer {
    background-image: url("../assets/trailer.jpg");
    background-size: cover;
    background-repeat: no-repeat;
    /* border-image: fill 0 linear-gradient(to top, rgba(0, 0, 0, 0.493), rgba(0, 0, 0, 0.5)); *
    transition: opacity 1s ease-in-out;
    position: relative;
    box-shadow: inset 0 0 0 1000px rgba(0, 0, 0, 0.5);
    box-shadow: 30px 30px 30px 30px rgba(0, 0, 0, 0.5);
    transition: 0.5s ease-in-out;
    transition: border-image 0.5s ease-in-out;
    border-radius: 5px;

}

.box-button-gallery {
    background-image: url("../assets/wallpaper.jpeg");
    background-size: cover;
    background-repeat: no-repeat;
    /*border-image: fill 0 linear-gradient(to top, rgba(0, 0, 0, 0.493), rgba(0, 0, 0, 0.5));*
    transition: opacity 1s ease-in-out;
    position: relative;
    box-shadow: inset 0 0 0 1000px rgba(0, 0, 0, 0.5);
    box-shadow: 30px 30px 30px 30px rgba(0, 0, 0, 0.5);
    transition: 0.5s ease-in-out;
    transition: border-image 0.5s ease-in-out;
    border-radius: 5px;

}



.color {
    background-color: #000000bb;
}

.book {
    width: 60%;
    margin: auto;
    max-width: 200%;

}


.container-dsc {
    display: inline-flex;
    /*margin: auto;
}*/

.desc {
    font-size: 1rem;
    font-family: 'Roboto', sans-serif;
    color: #f5f5f5;
    margin: auto;
    padding: 0;
    text-align: justify;
    text-justify: inter-word;
    line-height: 1.5;
    
    
    width: 100%;
    /*REVISAR*/
    display: inline-flex;
    justify-content: space-evenly;
    background-image: url("../assets/wallpaper.jpeg");
    border-image: fill 0 linear-gradient(to top, rgba(0, 0, 0, 0.493), rgba(0, 0, 0, 0.5));
    background-size: cover;



}
/*

.lore {
    margin: 5%;
    margin: auto;
    text-align: center;
    background-image: url("../assets/eldenskull.webp");
    height: 600px;
    background-attachment: fixed;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    border-image: fill 0 linear-gradient(to top, rgba(0, 0, 0, 0.493), rgba(0, 0, 0, 0.5));
    transition: opacity 1s ease-in-out;
    position: relative;


}

.lore-desc {
    font-size: 18px !important;
    width: 100%;
    font-family: "IBM Plex Mono", monospace;
    font-weight: 200;
    font-style: normal;
    background-color: rgba(0, 0, 0, 0.445);

}

.lore::before {
    content: "";
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    height: 50px;
   
    background: linear-gradient(to bottom, black, transparent);
}

.lore::after {
    content: "";
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    height: 50px;
   
    background: linear-gradient(to top, black, transparent);

}


.lore div {
    padding: 4rem;
    text-align: center;
    font-size: 20px;
    color: white;
    margin: auto;
    display: flex;
    border-radius: 50%;
    width: 90%;
    justify-content: center;

}

img {
    transition: transform 0.5s;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 10%;
    margin: auto;

}

a {
    text-decoration: none;
    color: #ffbf00;
    transition: 0.5s;
}

.container {
    display: flex;
    justify-content: space-around;
    align-items: center;
    margin-top: 10rem;
    padding-bottom: 0 !important;
}

 button {
    background: none;
    outline: none;
    border: none;
    color: #ffbf00;
    cursor: pointer;
    /*font-family: "Quicksand", sans-serif;*
    font-family: 'elden';
    font-optical-sizing: auto;
    font-weight: lighter;
    font-style: normal;
    font-size: 1.20em;
    letter-spacing: 0.3cap;


} 

a:hover {
    text-shadow: 0 0 30px #ebc20b;
    transition: 0.5s;
    color: aliceblue;

}

.buttons-container {
    display: flex !important;
    justify-content: space-between;
    align-items: center;
    width: 97% !important;
    margin: auto !important;

}*/
</style>
