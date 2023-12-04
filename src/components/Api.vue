<template>
	<div class="text-center font-serif">
<div class="text-center">
   <div class="flex items-center justify-center space-x-4">
	 <!-- Inicio de página -->
	   <div>
		<h1 class="text-3xl">SITMOTUL</h1>
		 <br>
		<h2 class="mb-2 text-xl"> Estado de la evaluación tutor del periodo {{ periodo }} al {{ obtenerFechaActual() }}</h2>
		  </div>
   </div>
		   
   <div class="flex items-center justify-center space-x-4 grid-cols-2">
		<div class="w-1/3">
		  <img class="w-2/3 h-auto mt-5" src="../../logo2.png" alt="Logo">
		</div>
		<!-- Datos de las tarjetas-->
		<div class="w-3/4">
		<!-- Tarjetas -->
		  <div class="flex justify-center space-x-10 mt-5">
		<!-- 1ra tarjeta vertical-->
		  <div class="w-3/2 bg-gradient-to-r p-2 rounded-lg" >
		<div v-for="(data, index) in infoGeneral" :key="index"
		class="" style="background-color: rgb(220, 150, 20);" h-full p-2 shadow-md rounded-md mb-2 flex items-center justify-center>
		  <div class="text-center">
   <i class="fa-solid fa-bell fa-shake" style="font-size: 50px; color: rgb(171, 6, 6);"></i>
		 <p class="mb-2 px-3 text-black font-bold text-2xl">Horas restantes para finalizar:
		  <p class="mb-2 px-3 text-white font-bold text-2xl">{{ calcularHorasRestantes(data.fin).horas }} Hrs.</p>
		</p>
		<p class="mb-2 px-3 text-black font-bold text-2xl"> Días restantes para finalizar:
		  <p class="mb-2 px-3 text-white font-bold text-2xl">{{ calcularHorasRestantes(data.fin).dias }} Días.</p>
		</p>
	   </div>
	   </div>
   <!-- 2da y 3ra tarjeta vertical-->
   <div v-for="(data, index) in infoGeneral" :key="index" class="flex space-x-12">
	   <div class="w-1/2 bg-gradient-to-r p-2 rounded-lg mb-5">
		 <div class="bg-green-600 p-4 shadow-md rounded-md">
		<p class="mb-2 px-3 text-white font-bold text-3xl"> {{ calcularPorcentaje(data.alEvaluados, data.alTotal) }} %</p>
	   <p class="font-semibold">{{ totalEvaluados }} Han respondido de {{ totalAlumnos }} 
	   <br> alumnos</p>
   <i class="fa-solid fa-chart-simple fa-beat-fade" style="color: #0603ac; font-size: 40px;"></i>
	   </div>
	</div>

   <div class="w-1/2 bg-gradient-to-r p-2 rounded-lg mb-5 flex space-x-12">
	   <div class=" bg-orange-400 p-8 shadow-md rounded-md">
	   <p class="b-2 px-3 text-white font-bold text-3xl">{{ calcularPorcentajeFaltante(data.alEvaluados, data.alTotal) }} % <i class="-triangle text-red-500"></i>
	   </p>
	   <p class="font-semibold"> {{ data.alTotal - data.alEvaluados }} Faltan responder de {{ data.alTotal }} alumnos</p>
	   <i class="fa-solid fa-restroom fa-beat" style="color: #094605; font-size: 40px;"></i>
	   </div>
	   </div>
   </div>
   </div>
</div>		
</div>
</div>
</div>

   <div class="w-2/7 grid grid-cols-1 gap-2"></div>
  <!-- Información de carreras -->
	   <div class="w-full from-slate-300 p-3 rounded-lg mt-2">
	   <h1 class="text-2xl text-center font-bold text-black">Estado de evalución por ingenierías</h1>
	   </div>
	<div class="w-12/12 m-auto h-auto dark:bg-gray-600 rounded-lg px-7 mt-10 mb-10">
   <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-5 gap-4 mx-3 bg-transparent">
	<!-- Tarjeta IEM -->
	   <div class="w-full  bg-gradient-to-r to-gray-200 p-3 rounded-lg mt-2">
		   <div class="w-1/">
			   <img class="w-3/2 h-auto mt-0" src="../../electromecanica.png" alt="Logo">
   </div>

   <div v-for="(data, index) in infoPersonal" :key="index" class="bg-white p-4 shadow-md rounded-md" style="border-radius: 25px;">
	   <div class="text-center">
			   <div v-if="data.IEM">
				<p>Respondido: {{ data.IEM.listas }} de 171. <br> {{ data.IEM.faltantes }} Pendientes </p>
			   </div>
		   </div>
		   </div>
	   </div>

<!-- Tarjeta IER -->
	   <div class="w-full  bg-gradient-to-r to-gray-200 p-3 rounded-lg mt-2">
		   <div class="w-1/">
		   <img class="w-3/2 h-auto mt-0" src="../../renovables.png" alt="Logo">
		   </div>

	   <div v-for="(data, index) in infoPersonal" :key="index" class="bg-white p-4 shadow-md rounded-md" style="border-radius: 25px;">
			   <div class="text-center">
			   <div v-if="data.IER">
				   <p>Respondido: {{ data.IER.listas }} de 101. <br> {{ data.IER.faltantes }} Pendientes</p>
			   </div>
		   </div>
		   </div>
	   </div>

   <!-- TarjetaII -->
	   <div class="w-full  bg-gradient-to-r to-gray-200 p-3 rounded-lg mt-2">
		   <div class="w-1/">
			   <img class="w-3/2 h-auto mt-0" src="../../industrial.png" alt="Logo">
		   </div>

		   <div v-for="(data, index) in infoPersonal" :key="index" class="bg-white p-4 shadow-md rounded-md" style="border-radius: 25px;">
			   <div class="text-center">
			   <div v-if="data.II">
				   <p>Respondido: {{ data.II.listas }} de 243. <br> {{ data.II.faltantes }} Pendientes</p>
			   </div>
		   </div>
		   </div>
	   </div>

	   <!-- Tarjeta deISC -->
	   <div class="w-full  bg-gradient-to-r  to-gray-200 p-3 rounded-lg mt-2">
		   <div class="w-1/">
			   <img class="w-3/2 h-auto mt-0" src="../../sistemas.png" alt="Logo">
		   </div>

		   <div v-for="(data, index) in infoPersonal" :key="index" class="bg-white p-4 shadow-md rounded-md" style="border-radius: 25px;">
			   <div class="text-center">
			   <div v-if="data.ISC">
				   <p>Respondido: {{ data.ISC.listas }} de 244. <br>{{ data.ISC.faltantes }} Pendientes</p>
			   </div>
		   </div>
		   </div>
	   </div>

<!-- Tarjeta IE -->
	   <div class="w-full  bg-gradient-to-r  to-gray-200 p-3 rounded-lg mt-2">
		   <div class="w-1/">
		   <img class="w-3/2 h-auto mt-0" src="../../electronica.png" alt="Logo">
		   </div>

	 <div v-for="(data, index) in infoPersonal" :key="index" class="bg-white p-4 shadow-md rounded-md" style="border-radius: 25px;">
		   <div class="text-center">
		   <div v-if="data.IE">
		   <p>Respondido: {{ data.IE.listas }} de 59 <br> {{ data.IE.faltantes }} Pendientes</p>
			   </div>
		   </div>
		   </div>
	   </div>
   </div>
</div>
</div>
</template>

   <script setup>
	 import { onMounted } from 'vue'
	import { ref } from 'vue'

 // Para nuestras variables
	const infoGeneral = ref([]) 
	const infoPersonal = ref([]) 

  const totalEvaluados = ref(0)
  const totalAlumnos = ref(0)
  const periodo = ref('')

 // Datos de la API
 async function fetchData(apiUrl, infoArray) {
try {
	   const response = await fetch(apiUrl)
	   const data = await response.json()
	   infoArray.value.push(data) 

	   totalEvaluados.value += data.alEvaluados || 0
	   totalAlumnos.value += data.alTotal || 0
	   if (!periodo.value) {
		   periodo.value = data.periodo || ''
	   }

	   console.log('Datos recibidos:', data)
	   
	   if (data.ObjectIE) {
		   console.log('ObjectIE:', data.ObjectIE)
	   }
	   if (data.IEM) {
		   console.log('IEM:', data.IEM)
	   }
	   if (data.IER) {
		   console.log('IER:', data.IER)
	   }
	   if (data.II) {
		   console.log('II:', data.II)
	   }
	   if (data.ISC) {
		   console.log('ISC:', data.ISC)
	   }
	   } catch (error) {
		console.error('Error al obtener datos:', error)
   }
}

onMounted(async () => {
   await fetchData('https://sitmotul.com.mx/api/statusEval', infoGeneral)
   await fetchData('https://sitmotul.com.mx/api/statusEvalIng', infoPersonal)
})

// Clcular  horas y días
const calcularHorasRestantes = (fechaFin) => {
   const ahora = new Date();
   const fechaFinalizacion = new Date(fechaFin);
   const diferenciaTiempo = fechaFinalizacion - ahora;
   const diferenciaDias = Math.floor(diferenciaTiempo / (1000 * 60 * 60 * 24));
   const diferenciaHoras = Math.floor(diferenciaTiempo / (1000 * 60 * 60));
   return {
	   dias: diferenciaDias >= 0 ? diferenciaDias : 0,
	   horas: diferenciaHoras >= 0 ? diferenciaHoras : 0,
   };
};

// Porcentaje
const calcularPorcentaje = (evaluados, total) => {
   if (total === 0) {
	   return 0;
   }
   return ((evaluados / total) * 100).toFixed(2);
};

const calcularPorcentajeFaltante = (evaluados, total) => {
   const faltantes = total - evaluados;
   if (total === 0 || faltantes <= 0) {
	   return 0;
   }
   return ((faltantes / total) * 100).toFixed(2);
};

//Obtener la fecha actual en el formato deseado
const obtenerFechaActual = () => {
   const opcionesFecha = {
	   weekday: "long",
	   day: "numeric",
	   month: "long",
	   year: "numeric",
   };
   const fechaActual = new Date();
   return fechaActual.toLocaleDateString("es-MX" - opcionesFecha);
};
</script>