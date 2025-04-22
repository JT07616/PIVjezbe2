<script setup>
const slike = {
  Jabuka: "https://www.svgrepo.com/show/530203/apple.svg",
  Mrkva: "https://www.svgrepo.com/show/530216/carrot.svg",
  Sir: "https://www.svgrepo.com/show/530219/cake.svg",
  Kruh: "https://www.svgrepo.com/show/530223/bread.svg",
};

const proizvodi = [
  { naziv: "Jabuka", cijena: 0.25 },
  { naziv: "Mrkva", cijena: 0.12 },
  { naziv: "Kruh", cijena: 2.0 },
  { naziv: "Sir", cijena: 4.48 },
];

const korisnik = {
  jeAdmin: true,
  osobni_podaci: {
    ime: "Marko",
    prezime: "Krivić",
    adresa: {
      grad: "Pula",
      ulica: "Veruda",
      broj: 32,
    },
    broj_telefona: "+091-123-456",
  },
  kosarica: [
    { naziv: "Jabuka", količina: 4 },
    { naziv: "Mrkva", količina: 12 },
    { naziv: "Sir", količina: 1 },
    { naziv: "Kruh", količina: 3 },
  ],
};

function dohvatiCijenu (naziv){
  const proizvod = proizvodi.find(p => p.naziv === naziv)
  return proizvod ? proizvod.cijena : 0
}

function dohvatiKolicinu(naziv) {
  const stavka = korisnik.kosarica.find(item => item.naziv === naziv);
  return stavka ? stavka.količina : 0;
}


function sveukupnaCijena() {
  let ukupno = 0;
  for (let i = 0; i < korisnik.kosarica.length; i++) {
    const stavka = korisnik.kosarica[i];
    const cijena = dohvatiCijenu(stavka.naziv);
    ukupno += cijena * stavka.količina;
  }
  return ukupno;
}
S
function najskupljaStavka(){
  let max = 0;
  let nazivNaj = ""
  for(let i = 0 ; i<korisnik.kosarica.length ; i++){
      const stavka = korisnik.kosarica[i]
      const cijena = stavka.količina * dohvatiCijenu(stavka.naziv)


    if(cijena > max){
      max = cijena;
      nazivNaj = stavka.naziv;
    }
  }
  return nazivNaj;
}



</script>

<template>
 <div class = 'flex flex-col gap-2 h-full  justify-center items-center w-300'>
   <div :class = "['bg-[#f1f5f9] p-4 rounded-md w-96', korisnik.jeAdmin ? 'text-blue-700' : 'text-black']">
   <p >Korisnički podaci</p>
   <hr class ="my-3 ">
   <p><span class="font-bold">Ime: </span>{{ korisnik.osobni_podaci.ime }} {{ korisnik.osobni_podaci.prezime }}</p>
   <p><span class="font-bold">Adresa: </span>{{ korisnik.osobni_podaci.adresa.ulica }} {{ korisnik.osobni_podaci.adresa.broj }}, {{ korisnik.osobni_podaci.adresa.grad }}</p>
   <p><span class="font-bold">Telefon: </span>{{ korisnik.osobni_podaci.broj_telefona }} </p>


   </div>

   <div class="flex flex-col gap-2 bg-[#f1f5f9] p-4 rounded-lg w-96">
  <h1 class="font-bold">🛒 Košarica</h1>

  
  <ul class="flex flex-col gap-2">
    <li :class="['border flex border-gray-500 items-center gap-4 p-2 rounded-md' , najskupljaStavka() === 'Jabuka' ? 'bg-red-100 border-red-400' : ''  ]">
      <img :src="slike.Jabuka" class="w-20 h-20">
      <div class="text-sm text-gray-800">
        <p class="font-bold">Jabuka</p>
        <p>Cijena: €{{ dohvatiCijenu('Jabuka') }} | Količina: {{ dohvatiKolicinu('Jabuka') }}</p>
        <p>Ukupno: €{{ (dohvatiCijenu('Jabuka') * dohvatiKolicinu('Jabuka')).toFixed(2)  }}</p>
      </div>
    </li>

    <li :class="['border flex border-gray-500 items-center gap-4 p-2 rounded-md' , najskupljaStavka() === 'Mrkva' ? 'bg-red-100 border-red-400' : ''  ]">
      <img :src="slike.Mrkva" class="w-20 h-20">
      <div class="text-sm text-gray-800">
        <p class="font-bold">Mrkva</p>
        <p>Cijena: €{{ dohvatiCijenu('Mrkva') }} | Količina: {{ dohvatiKolicinu('Mrkva') }}</p>
        <p>Ukupno: €{{ (dohvatiCijenu('Mrkva') * dohvatiKolicinu('Mrkva')).toFixed(2)  }}</p>
      </div>
    </li>

    <li :class="['border flex border-gray-500 items-center gap-4 p-2 rounded-md' , najskupljaStavka() === 'Kruh' ? 'bg-red-100 border-red-400' : ''  ]">
      <img :src="slike.Kruh" class="w-20 h-20">
      <div class="text-sm text-gray-800">
        <p class="font-bold">Kruh</p>
        <p>Cijena: €{{ dohvatiCijenu('Kruh') }} | Količina: {{ dohvatiKolicinu('Kruh') }}</p>
        <p>Ukupno: €{{ (dohvatiCijenu('Kruh') * dohvatiKolicinu('Kruh')).toFixed(2)  }}</p>
      </div>
    </li>

    <li :class="['border flex border-gray-500 items-center gap-4 p-2 rounded-md' , najskupljaStavka() === 'Sir' ? 'bg-red-100 border-red-400' : '' ]">
      <img :src="slike.Sir" class="w-20 h-20">
      <div class="text-sm text-gray-800">
        <p class="font-bold">Sir</p>
        <p>Cijena: €{{ dohvatiCijenu('Sir') }} | Količina: {{ dohvatiKolicinu('Sir') }}</p>
        <p>Ukupno: €{{ (dohvatiCijenu('Sir') * dohvatiKolicinu('Sir')).toFixed(2)  }}</p>
      </div>
    </li>
  </ul>

  
  <div class="font-bold mt-4">
    <p>Ukupna cijena: €{{ sveukupnaCijena()  }}</p>
  </div>
</div>
</div>

</template>

<style scoped>

</style>
