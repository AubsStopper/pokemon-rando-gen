<template>
    <div>
    <button v-on:click="modalShow = !modalShow">More Info</button>
        <div v-show="modalShow" >
            <div class="modal-mask">
                <div class="modal-wrapper">
                    <div class="modal-container">
                        <div> name : {{ wholechar.name }} </div>
                        <div> weight: {{ wholechar.weight }} </div>
                        <div> </div>
                        <div>
                            <!-- <img v-bind:src="wholechar.sprites.front_default">    -->
                        </div>

                        <!-- <div> {{ wholechar.types}} </div> -->

                        <button v-on:click="modalShow = !modalShow"> Close </button>
                        
                    </div>    
                </div>
            </div>    
        </div> 
    </div>
</template>

<script>

export default {
    data() {
        return {
            modalShow: false,
            img: undefined
        }
    },
    props: {
        wholechar: {}
    },
    computed: {
      
    }
}
</script>

<style scoped>

.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
  height: 80%;
}

.modal-container {
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}
</style>