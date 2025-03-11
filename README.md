<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Félix-Antoine Coutu</title>
<style>
   body {
       font-family: Arial, sans-serif;
       text-align: center;
       padding: 10px;
   }

   /* Changer la taille de la police pour les titres */
   h1 {
      font-size: 16px !important;  /* Ajuste la taille ici comme tu le souhaites */
      font-weight: bold;
      color: #333;  /* Facultatif : change la couleur si nécessaire */
      margin: 0;  /* Empêche les marges par défaut entre les h1 */
      border: none;  /* Enlève les bordures */
   }
   /* Si tu veux ajouter des espacements spécifiques entre les deux titres */
   .titre-1 {
       margin-bottom: 16px;  /* Ajoute un espace après le premier titre */
   }

   .video-container {
      position: relative;
      display: inline-block;
   }

   video {
      width: 100%;
      max-width: 2000px;
   }

   .btn-video {
    position: absolute;
    top: 10px;
    left: 10px; /* Alignement parfait en haut à gauche */
    width: 150px; /* Taille fixe du bouton */
    height: 30px; /* Hauteur fixe */
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #433d69;
    color: white;
    font-size: 12px;
    font-weight: bold;
    border: none;
    cursor: pointer;
    border-radius: 3px;
    opacity: 0.8;
    transition: opacity 0.2s, background-color 0.3s;
    z-index: 10;
   }

   .btn-video:hover {
       opacity: 1;
   }

   .btn-salle1 {
       background-color: #194f18;
   }

   .btn-salle2 {
       background-color: #433d69;
   }
</style>
</head>
<body>

<h1 class="titre-1">Fumée Omnisciente, Mirage Onirique | Résidence de création, janvier 2025, Bain Mathieu</h1>

<div class="video-container">
   <video id="video" controls>
      <source src="https://dl.dropboxusercontent.com/scl/fi/vn856dku4ckgm35azhbz1/Fumee-Omnisciente-Mirage-Onirique02.mp4?rlkey=khuru1f6c5woeclemz1ai9rlz&st=pksoqe29&raw=1" type="video/mp4">    
      Votre navigateur ne prend pas en charge la vidéo HTML5.
   </video>

   <button id="btnBascule" class="btn-video">Audio salle de droite</button>
</div>

<audio id="audioSalle1" preload="none">
   <source src="https://www.dropbox.com/scl/fi/ur8dl9pxqmyqqcgq63a2l/FOMO_Audio_Perfo-res-Bain-Mathieu_DRUM.mp3?rlkey=oendf779ij0ijz57i5z65vb8h&st=wya35hdc&raw=1" type="audio/mp3">
</audio>

<audio id="audioSalle2" preload="none">
   <source src="https://www.dropbox.com/scl/fi/vxsx4wc0ojrao15vsi3rd/FOMO_Audio_Perfo-res-Bain-Mathieu_INSTALL.mp3?rlkey=yuieg0gk2a5t0b6kquxjgoav4&st=15anchfs&raw=1" type="audio/mp3">
</audio>

<script>

   var video = document.getElementById("video");
   var audioSalle1 = document.getElementById("audioSalle1");
   var audioSalle2 = document.getElementById("audioSalle2");
   var btnBascule = document.getElementById("btnBascule");
   
   var audioActif = audioSalle2;
   btnBascule.classList.add("btn-salle2");
   
   // Désactiver le premier audio au démarrage
   audioSalle1.src = ""; 
   
   function synchroniserAudio() {
       var diff = Math.abs(video.currentTime - audioActif.currentTime);
       if (diff > 0.3) {
           audioActif.currentTime = video.currentTime;
       }
   }
   
   // Gestion de la lecture et pause synchronisée
   video.addEventListener("play", function () {
       if (audioActif.src) {
           audioActif.currentTime = video.currentTime;
           audioActif.play();
       }
   });
   
   video.addEventListener("pause", function () {
       if (audioActif.src) {
           audioActif.pause();
       }
   });
   
   video.addEventListener("timeupdate", synchroniserAudio);
   
   // **BOUTON POUR CHANGER L'AUDIO**
   btnBascule.addEventListener("click", function () {
       // Désactiver complètement l'audio actif
       if (audioActif.src) {
           audioActif.pause();
           audioActif.src = ""; // Libère la mémoire
       }
   
       // Basculer vers l'autre piste
       if (audioActif === audioSalle1) {
           audioActif = audioSalle2;
           audioActif.src = "https://www.dropbox.com/scl/fi/vxsx4wc0ojrao15vsi3rd/FOMO_Audio_Perfo-res-Bain-Mathieu_INSTALL.mp3?rlkey=yuieg0gk2a5t0b6kquxjgoav4&st=15anchfs&raw=1";
           btnBascule.textContent = "Audio salle de droite";
           btnBascule.classList.remove("btn-salle1");
           btnBascule.classList.add("btn-salle2");
       } else {
           audioActif = audioSalle1;
           audioActif.src = "https://www.dropbox.com/scl/fi/ur8dl9pxqmyqqcgq63a2l/FOMO_Audio_Perfo-res-Bain-Mathieu_DRUM.mp3?rlkey=oendf779ij0ijz57i5z65vb8h&st=wya35hdc&raw=1";
           btnBascule.textContent = "Audio salle de gauche";
           btnBascule.classList.remove("btn-salle2");
           btnBascule.classList.add("btn-salle1");
       }
   
       // Synchroniser avec la vidéo immédiatement
       if (!video.paused) {
           audioActif.currentTime = video.currentTime;
           audioActif.play();
       }
   });

</script>

</body>
</html>
