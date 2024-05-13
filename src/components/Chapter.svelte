<script>
    import WallScrolly from "$components/WallScrolly.svelte";
    import ChapterText from "$components/ChapterText.svelte";
    import Bookmark from "$components/Bookmark.svelte";
    import inView from "$actions/inView.js";
    import { activeSection } from "$stores/misc.js";
    import { fly } from 'svelte/transition';
	import YardsaleScrolly from "./Yardsale.scrolly.svelte";

    import f01_esquerda from "$images/esquerda/f01d.jpg";
    import f02_esquerda from "$images/esquerda/f03.jpg";
    import f03_esquerda from "$images/esquerda/f02b.jpg";
    import f04_esquerda from "$images/esquerda/f04.jpg";
    import f05_esquerda from "$images/esquerda/f05.jpg";

    import f01_direita from "$images/direita/f01b.jpg";
    import f02_direita from "$images/direita/f03.jpg";
    import f03_direita from "$images/direita/f02.jpg";
    import f04_direita from "$images/direita/f04.jpg";
    import f05_direita from "$images/direita/f05.jpg";
  
    import { fade } from 'svelte/transition';
    
    let currentImageEsquerda = f01_esquerda;
    let currentImageDireita = f01_direita;

	let scrollDir;
	let lastY;
    let headlingFly = false;

    function getLegenda() {
    if (currentImageEsquerda === f01_esquerda) {
      return 'legenda 1';
    } else if (currentImageEsquerda === f05_esquerda) {
      return 'legenda 2';
    } else if (currentImageEsquerda === f04_esquerda) {
      return 'legenda 3';
    } else if (currentImageEsquerda === f03_esquerda) {
      return 'legenda 4';
    } else if (currentImageEsquerda === f02_esquerda) {
      return 'legenda 5';
    }

    // Caso nenhuma condição seja correspondida, retorne uma legenda padrão
    return 'legenda padrão';

  }

    let scrolly1 = [
        "The Future Arena hosted the Handball competitions at the Olympics and Goalball at the Paralympics in 2016.",
        "",
        "",
        "And it was not named this way for nothing: its name has everything to do with what it was intended to become. ",
        "",
        "",
        "In March 2022, the dismantling of the Arena began to be transformed into four schools in the West Zone.",
        "",
        "",
        "Materials such as breeze (arena facade), partitions, and dishes were reused from the Future Arena.",
        "",
        "",
        "Two of the four planned gyms have already been inaugurated: the GET (Technological Experimental Gymnasium) José Mauro de Vasconcelos, in Bangu, and the GET Emiliano Galdino, in Santa Cruz.",
        "",
        "",
        "The other two schools, which are being built in the Campo Grande and Rio das Pedras neighborhoods, are scheduled to open in the first semester of this year.",
        "",
        "",
        "The educational units have the most innovative public school model in the country, following the STEAM approach (Science, Technology, Engineering, Arts, and Mathematics).",
        "",
        "",
        "This model invests in the qualification of integral education and develops project-based learning, hands-on activities, and resources that promote digital culture.",
        "",
        "",
        "",
        "nova-escola"
  ]

    export let id;
    export let copyBlock;
    export let scrollY;

    function setSectionEnter(id) { 
        headlingFly = true;
        activeSection.set(id); 
    }
    function setSectionExit(id) { 
        let nextSection;
        if (scrollDir == "down") {
            if (id == "raunchiness") { nextSection = "illustration"; } 
            else if (id == "illustration") { nextSection = "race"; }
            else if (id == "race") { nextSection = "methods"; }
            activeSection.set(nextSection)
        } else if (scrollDir == "up") {
            if (id == "raunchiness") { nextSection = "intro"; } 
            else if (id == "illustration") { nextSection = "raunchiness"; }
            else if (id == "race") { nextSection = "illustration"; }
            activeSection.set(nextSection)
        }
    }

    function checkScrollY(scrollY) {
        if (scrollY) {
            scrollDir = scrollY > lastY ? "down" : "up"
            lastY = scrollY;
        }
    }

    
    $: scrollY, checkScrollY(scrollY);

    let legenda;
    let legenda2;
    let legendaEsquerda;
    let legendaDireita;

$: {
    if (currentImageEsquerda === f01_esquerda) {
      legenda = 'See what happened to the Arena of the Future';
      legenda2 = 'Click on the buttons below';
      legendaEsquerda = 'Arena of the Future';
      legendaDireita = 'Experimental Technological Gymnasiums';
    } else if (currentImageEsquerda === f05_esquerda) {
      legenda = 'Bleachers';
      legenda2 = "Below we see the bleachers of the Arena of the Future. They were designed in a precast concrete structure that allows for assembly and disassembly, similar to the metal structure of the roof. These elements were donated to the Luso-Brasileiro Stadium, owned by Portuguesa-RJ, on Ilha do Governador. The donation will allow increasing the venue's capacity from 5,044 to 16,000 spectators.";
      legendaEsquerda = 'Arena of the Future';
      legendaDireita = 'Estádio Luso-Brasileiro';
    } else if (currentImageEsquerda === f04_esquerda) {
      legenda = 'Facade';
      legenda2 = 'In the image below, we highlight the brise that composes the facade of the Arena of the Future. This element allows natural ventilation while providing protection from solar incidence. The brises were reused in four schools (Experimental Technological Gymnasiums), located in the neighborhoods of Bangu, Campo Grande, Rio das Pedras, and Santa Cruz.';
      legendaEsquerda = 'Arena of the Future';
      legendaDireita = 'Experimental Technological Gymnasiums';
    } else if (currentImageEsquerda === f03_esquerda) {
      legenda = 'Partitions';
      legenda2 = 'The partitions of the Arena of the Future are internal walls of the spaces, composed of a metal substructure and a closure in plasterboard (drywall), allowing their installation to be done through fittings and screws. These walls were reused in four schools (Experimental Technological Gymnasiums), located in the neighborhoods of Bangu, Campo Grande, Rio das Pedras, and Santa Cruz.';
      legendaEsquerda = 'Arena of the Future';
      legendaDireita = 'Experimental Technological Gymnasiums';
    } else if (currentImageEsquerda === f02_esquerda) {
      legenda = 'Fixtures';
      legenda2 = 'The bathroom fixtures of the Arena of the Future, such as sinks, toilets, and urinals, were reused in four schools (Experimental Technological Gymnasiums), located in the neighborhoods of Bangu, Campo Grande, Rio das Pedras, and Santa Cruz.';
      legendaEsquerda = 'Arena of the Future';
      legendaDireita = 'Experimental Technological Gymnasiums';
    } else {
      legenda = 'legenda padrão';
    }
}
</script>

<section id={id}
    use:inView={{ top: 0 }}
    on:enter={() => setSectionEnter(id)}
    on:exit={() => setSectionExit(id)}>
    {#if headlingFly }
        <!-- <h2 in:fly={{ y: 200, duration: 2000 }}>{resetTitles(id)}</h2> -->
        {#if id == "raunchiness"}
            <YardsaleScrolly words={scrolly1} container="scrolly1"  />
        {/if}
        {#if id == "illustration"}
        <div class="legendas">
        <div class="legenda"> {legenda}</div>
        {#if legenda2 == 'Click on the buttons below' }
        <div class="legenda2combotao"> 
          <span>Click on the buttons &nbsp&nbsp </span>
          <button data-tooltip="Botão" class="image-button-example">+</button>
          <span>&nbsp &nbsp below</span>
        </div>
        {:else}
        <div class="legenda2"> {legenda2}</div>
        {/if}
       </div>
        <div class="container">
            <div class="image-container">
                <img class="img2_left" src={currentImageEsquerda} alt="img2_left" in:fade={{ delay: 0 }} out:fade />
                <div class="primeira-imagem">
                  <p style="display:flex;align-items:center">{legendaEsquerda}</p>
                </div>
               <!--reseta / images iniciais-->
                <!-- <button data-tooltip="Click on the buttons" class="image-button" style="top: 68%; left: 63%;" on:click={() => (currentImageEsquerda = f01_esquerda) && (currentImageDireita = f01_direita)}>+</button> -->
                <!--arquibancada-->
                <button data-tooltip="Bleachers" class="image-button" style="top: 53%; left: 40%;" on:click={() => (currentImageEsquerda = f05_esquerda) && (currentImageDireita = f05_direita)}>+</button>
                <!--Facade-->
                <button data-tooltip="Facade" class="image-button" style="top: 65%; left: 10%;" on:click={() => (currentImageEsquerda = f04_esquerda) && (currentImageDireita = f04_direita)}>+</button>
                <!--drywall-->
                <button data-tooltip="Partitions" class="image-button" style="top: 77%; left: 30%;" on:click={() => (currentImageEsquerda = f03_esquerda) && (currentImageDireita = f03_direita)}>+</button>
               <!--Fixtures-->
                <button data-tooltip="Fixtures" class="image-button" style="top: 53%; left: 90%;" on:click={() => (currentImageEsquerda = f02_esquerda) && (currentImageDireita = f02_direita)}>+</button>
            </div>
            <div class="image-container">
            <img src={currentImageDireita} alt="currentImage" in:fade={{ delay: 0 }} out:fade />
            <div class="segunda-imagem">
              <p style="display:flex;align-items:center">{legendaDireita}</p>
          </div>
          </div>
        </div>
        {/if}
    {/if}
    <ChapterText copy={copyBlock}/>
</section>

<style>
  .image-button:hover::after {
    margin-bottom: 3px;
    content: attr(data-tooltip);
    position: absolute;
    bottom: 100%;
    left: 50%;
    transform: translateX(-50%);
    background-color: black;
    color: white;
    padding: 4px 8px;
    border-radius: 4px;
    font-size: 12px;
    white-space: nowrap;
    z-index: 1;
    /* Additional styling as needed */
}
  .image-button-example:hover::after {
    margin-bottom: 3px;
    content: attr(data-tooltip);
    position: absolute;
    bottom: 100%;
    left: 50%;
    transform: translateX(-50%);
    background-color: black;
    color: white;
    padding: 4px 8px;
    border-radius: 4px;
    font-size: 12px;
    white-space: nowrap;
    z-index: 1;
    /* Additional styling as needed */
}
  .segunda-imagem{
    display: flex;
    justify-content: flex-end;
    padding-right: 1.5rem;
    margin-top: -3rem;
    color: #333; 
    font-size: 1.5rem;
    font-weight: bold;
  }
  .primeira-imagem{
    display: flex;
    justify-content: flex-start;
    padding-left: 1.5rem;
    margin-top: -3rem;
    color: #333; 
    font-size: 1.5rem;
    font-weight: bold;
  }
.legenda{
    display: flex;
    justify-content:center;
    /* flex-direction: column; */
    max-width: 90rem;
    margin: 0 auto;
    padding: 1rem; 
    color: #333; 
    /* margin-bottom: 20px !important; */
    font-size: 1.8rem;
    font-weight: bold;
    /* text-decoration: underline; */
}
.legenda2{
    display: flex;
    justify-content:center;
    text-align: center;
    /* flex-direction: row; */
    max-width: 48rem;
    min-height: 155px;
    margin: 0 auto;
    padding: 1rem; 
    color: #333; 
    margin-top: -20px !important;
    font-size: var(--16px);
    
}
.legenda2combotao{
  min-height: 155px;
    display: flex;
    justify-content:center;
    text-align: center;
    /* flex-direction: row; */
    max-width: 48rem;
    margin: 0 auto;
    padding: 1rem; 
    color: #333; 
    margin-top: -20px !important;
    font-size: var(--16px);
    
}
@media (max-width: 640px) {
    .legenda {
        text-align: center;
        /* margin-left: -1rem; */
    }
    .legenda2 { 
        min-height: 300px;
        display: flex;
        justify-content:center;
        text-align: center;
        font-weight:lighter
    }
    .legenda2combotao {
      min-height: 300px;
        text-align: left;
        margin-left: -1rem;
    }
    .primeira-imagem{
    display: flex;
    justify-content: center;
    margin-left: -1rem;
    font-size: 1.3rem;
  }
    .segunda-imagem{
    display: flex;
    justify-content: center;
    text-align: center;
    margin-left: 1rem;
    font-size: 1.3rem;
  }
}
.container {
  margin: 0 auto;
  display: flex;
  justify-content: flex-start;
  width: 100%;
}

.container .image-container, .container img {
  width: 50%;
  flex: 1;
}

.image-container {
  position: relative;
}

.image-container img {
  width: 100%;
}

/* Adicione esta consulta de mídia para alterar a largura em dispositivos móveis */
@media screen and (max-width: 640px) {
  .container .image-container, .container img {
    width: 100%;
  }
}

.image-button {
  position: absolute;
  width: 30px; 
  height: 30px; 
  border-radius: 50%;
  background-color: black;
  text-align: center;
  padding: 0;
  border: none;
  color: white;
  font-size: 20px; 
}
.image-button-example {
  /* position: absolute; */
  width: 30px; 
  height: 30px; 
  border-radius: 50%;
  background-color: black;
  text-align: center;
  padding: 0;
  border: none;
  color: white;
  font-size: 20px; 
}

@media (max-width: 640px) {
  .container {
    flex-direction: column;
  }

  .container img {
    width: 100%;
  }
}
    section {
        padding: 3rem 0;
    }
    #raunchiness {
        /* background-image: linear-gradient(var(--romance-bg-pink) 0%, var(--romance-bg-blue) 10%); */
    }
    #illustration {
        /* background-image: linear-gradient(var(--romance-bg-blue) 0%, var(--romance-bg-yellow) 10%); */
    }
    #race {
        /* background-image: linear-gradient(var(--romance-bg-yellow) 0%, var(--romance-bg-teal) 10%); */
    }
    :global(section a) {
		color: var(--color-gray-800);
		background-repeat: no-repeat;
        transition: background-position .08s ease-out;
        background-position: 0 1.125rem;
		border-bottom: none;
		pointer-events: auto;
	}
    :global(#raunchiness a) {
		/* background-image: linear-gradient(180deg,transparent 0,var(--romance-blue-light) 0); */
	}
	:global(#illustration a) {
		/* background-image: linear-gradient(180deg,transparent 0,var(--romance-yellow-light) 0); */
	}
	:global(#race a) {
		/* background-image: linear-gradient(180deg,transparent 0,var(--romance-teal-light) 0); */
	}
    :global(#intro a) {
		/* background-image: linear-gradient(180deg,transparent 0,var(--romance-pink-light) 0); */
	}
    :global(#methods a) {
        /* background-image: linear-gradient(180deg,transparent 0,var(--romance-pink-light) 0); */
        background-position: 0 1.05rem;
    }
    :global(section a:hover) {
		background-position: 0 0;
	}
    h2 {
        display: flex;
        justify-content: center;
        flex-direction: column;
        width: 100%;
        margin: 0 auto 4rem auto;
        text-align: center;
        text-transform: capitalize;
        font-family: var(--serif-display);
        font-size: var(--44px);
        padding: 3rem 0 0 0;
        z-index: 100;
        position: relative;
        overflow: hidden;
        min-height: 15rem;
    }
    h2:after {
        position: absolute;
        font-family: var(--sans-display);
        font-weight: 900;
        font-size: 200px;
        text-align: center;
        left: 50%;
        transform: translate(-50%, -10%);
        text-transform: uppercase;
        pointer-events: none;
        z-index: -1;
        letter-spacing: -0.5rem; 
    }
    /* :global(#raunchiness h2:after) {
        content: "Raunchiness";
        background: linear-gradient(to bottom, rgba(142, 172, 249, 0) 15%, rgba(142, 172, 249, 1));
        -webkit-text-fill-color: transparent;
        -webkit-background-clip: text;
        opacity: 0.25;
    }
    :global(#illustration h2:after) {
        content: "Illustration";
        background: linear-gradient(to bottom, rgba(253, 229, 154, 0) 15%, rgba(253, 229, 154, 1));
        -webkit-text-fill-color: transparent;
        -webkit-background-clip: text;
        opacity: 0.5;
    }
    :global(#race h2:after) {
        content: "Diversity";
        background: linear-gradient(to bottom, rgba(124, 231, 231, 0) 15%, rgba(124, 231, 231, 1));
        -webkit-text-fill-color: transparent;
        -webkit-background-clip: text;
        opacity: 0.35;
    } */
    @media only screen and (min-width: 600px) {
        section {
            padding: 3rem 0;
        }
        h2 {
            font-size: var(--64px);
        }
        h2:after {
            font-size: 300px;
        }
	}
</style>