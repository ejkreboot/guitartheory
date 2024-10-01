<script>
  import * as fretboard from "fretboards";
  import { draw } from "vexchords";
  import { chords } from "$lib/chords.js";
  import { onMount } from "svelte";
  import * as fretful from "$lib/fretful.js"

  let chordName = "D7";
  var E_triads = fretful.transpose_triplets(fretful.minor_triplets.top, 4, 14).join(" ");
  var D_triads = fretful.transpose_triplets(fretful.minor_triplets.top, 2, 14).join(" ");
  var A_triads = fretful.transpose_triplets(fretful.minor_triplets.top, 9, 14).join(" ");

  const updateChord = function () {
    const chord = chords.filter((c) => c.name == chordName)[0];
    if (!chord) {
      return;
    }
    document.querySelector("#chord").innerHTML = "";
    draw("#chord", chord, {
      width: 90,
      height: 120,
      defaultColor: "#000",
      showTuning: false,
    });
  };

  onMount(() => {
    fretboard.Fretboard.drawAll(".fb-container", {
      radius: 6,
      fretboardColor: "#111",
      fretHeight: 15,
      fretWidth: 35,
      dotSize: 12,
    });
    updateChord();
  });
</script>

<style>
      /* some colors: #f95e2e #80cbe0 #faa336 #739afc */
      body {
        font-family: "Open Sans", Helvetica;
      }

      p {
        padding-top: 10px;
      }

      @media print {
            .no-print {
                  display: none;
            }
      }
</style>

<body>

<div class="no-print">
      <input size=10 bind:value={chordName} on:keyup={updateChord}>
      <div id="chord"></div>      
</div>

<p>A minor hexatonic (blues) scale</p>
  <div class="fb-container"
        data-frets=14
        data-showNames=true
        data-radius=6
        data-colors="red gray gray blue gray gray gray gray"
        data-notes="a minor-blues">
  </div>
  <p>A minor triads</p>
  <div class="fb-container"
  data-frets=14
  data-showNames=true
  data-namecolors="black"
  data-notes="{A_triads}"
  data-fillcolors= "#f95e2e #f95e2e #f95e2e #80cbe0 #80cbe0 #80cbe0 #faa336 #faa336 #faa336 #efbdac #efbdac #efbdac"
  >
  </div>

  <p>D minor triads</p>
  <div class="fb-container"
  data-frets=14
  data-showNames=true
  data-namecolors="black"
  data-notes="{D_triads}"
  data-fillcolors= "#f95e2e #f95e2e #f95e2e #80cbe0 #80cbe0 #80cbe0 #faa336 #faa336 #faa336 #efbdac #efbdac #efbdac"
  >
  </div>

  <p>E minor triads</p>
  <div class="fb-container"
  data-frets=14
  data-showNames=true
  data-namecolors="black"
  data-notes="{E_triads}"
  data-fillcolors= "#f95e2e #f95e2e #f95e2e #80cbe0 #80cbe0 #80cbe0 #faa336 #faa336 #faa336 #efbdac #efbdac #efbdac"
  >
  </div>


</body>