<template>

<div class="w-screen h-screen flex items-center justify-center bg-gray-100 dark:bg-black">
  <div class="w-full mx-auto py-16">
    <!-- Title -->
    <h1 class="text-3xl text-center font-bold mb-6 dark:text-white">Slot Machine</h1>
    <!-- End Title -->
    <!-- Slot Machine -->
    <div v-if="tokens > 0" class="bg-white px-6 py-4 my-3 w-1/4 mx-auto shadow rounded-md">
      <div class="grid grid-cols-3 gap-2 mx-auto w-full block p-2 pb-20 justify-items-center">
        <div v-for="(spinre, index) in spinre" :key="index">
            <p>{{ spinre }}</p>
        </div>
      </div>
      <div class="w-full text-center mx-auto block">
        <p>Betting: {{ bet }} | Tokens: {{tokens}}</p>
        <button @click="spin()" type="button" class="border border-green-500 text-green-500 rounded-md px-4 py-2 m-2 transition duration-500 ease select-none hover:text-white hover:bg-green-600 focus:outline-none focus:shadow-outline my-4 mt-8">Spin</button>
        <p class="pt-6">Select Bet Amount</p>
        <button @click="bet = 1" type="button" class="border border-gray-300 text-gray-700 rounded-md px-4 py-2 m-2 transition duration-500 ease select-none hover:bg-gray-300 focus:outline-none focus:shadow-outline"> 1</button>
        <button @click="bet = 5" type="button" class="border border-gray-300 text-gray-700 rounded-md px-4 py-2 m-2 transition duration-500 ease select-none hover:bg-gray-300 focus:outline-none focus:shadow-outline"> 5</button>
        <button @click="bet = 10" type="button" class="border border-gray-300 text-gray-700 rounded-md px-4 py-2 m-2 transition duration-500 ease select-none hover:bg-gray-300 focus:outline-none focus:shadow-outline"> 10</button>
        <button @click="bet = 15" type="button" class="border border-gray-300 text-gray-700 rounded-md px-4 py-2 m-2 transition duration-500 ease select-none hover:bg-gray-300 focus:outline-none focus:shadow-outline"> 15</button>
        <button @click="bet = 20" type="button" class="border border-gray-300 text-gray-700 rounded-md px-4 py-2 m-2 transition duration-500 ease select-none hover:bg-gray-300 focus:outline-none focus:shadow-outline"> 20</button>
      </div>
    </div>

    <div v-else class="bg-white px-6 py-4 my-3 w-1/4 mx-auto shadow rounded-md text-center justify-items-center block">
       <p> You Lost</p>
        <button @click="tokens = 50" class=" border border-gray-300 text-gray-700 rounded-md px-4 py-2 m-2 transition duration-500 ease select-none hover:bg-gray-300 focus:outline-none focus:shadow-outline">Restart with 50 Tokens</button>
    </div>
    <!-- End Outline -->
  </div>
</div>


</template>

<script>
export default {
  name: "slotMachine",
    // mounted() {
    //     console.log('Component mounted.')
    // },
    props: {

    },
    data(){
        return{
            bet: 1,
            tokens: 50,
            score: [
                { data: [1.,1,1], value: 5 },
                { data: [2.,2,2], value: 10},
                { data: [3.,3,3], value: 20},
                { data: [4.,4,4], value: 40 },
            ],
            spinre: [0,0,0],
        }
    },
    methods: {
        spin(){
            let rnd = [this.getRandomInt(4),this.getRandomInt(4),this.getRandomInt(4)];
            this.spinre = rnd;
            this.tokens -= this.bet;
            for (var i = 0; i < this.score.length; ++i) {
                let current = this.score[i]
                if (JSON.stringify(current.data) === JSON.stringify(rnd)) {
                    this.tokens += (current.value * this.bet);
                }
                else{
                    for (var j = 0; j < rnd.length; ++j) {
                        this.tokens += Number(rnd[j]);
                    }
                }
            }
            return rnd;
        },
        getRandomInt(max){
            return Math.floor(Math.random() * Math.floor(max));
        }
  }
};
</script>