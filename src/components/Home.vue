<template>

    <div>
       <body>
    <header>
        <span>123Game</span>
        <button class="btn" @click="replay">New Game</button>
    </header>
        
    <div class="container">
    
        <div class="left">
            <div class="row-1" id="row1">
                <div style="background:rgb(215, 136, 221);" class="box-1" @click="changeVal(1,'rgb(215, 136, 221)')"  id="b1">1</div>
                <div style="background:rgb(136, 221, 159) ;" class="box-1" @click="changeVal(2,'rgb(136, 221, 159)')" id="b2">2</div>
                <div style="background:rgb(113, 124, 47) ;" class="box-1" @click="changeVal(3,'rgb(113, 124, 47)')" id="b3">3</div>
                <div style="background:rgb(124, 56, 11) ;" class="box-1" @click="changeVal(4,'rgb(124, 56, 11)')" id="b4">4</div>
                <div style="background:rgb(97, 88, 219) ;" class="box-1" @click="changeVal(5,'rgb(97, 88, 219)')" id="b5">5</div>
                
            </div>
            <div class="row-1">
                <div style="background:rgb(223, 15, 143) ;" class="box-1" @click="changeVal(6,'rgb(223, 15, 143)')" id="b6">6</div>
                <div style="background:rgb(58, 66, 60) ;" class="box-1" @click="changeVal(7,'rgb(58, 66, 60)')" id="b7">7</div>
                <div style="background: rgb(220, 20, 60);" class="box-1" @click="changeVal(8,'rgb(220, 20, 60)')" id="b8">8</div>
                <div style="background: rgb(238, 226, 61);" class="box-1" @click="changeVal(9,'rgb(238, 226, 61)')" id="b9">9</div>
            </div><br>
            <div class="txt" id="moves"> {{moves}} moves left</div>
            
    
        </div>

        <div class="right" id="right">
            <div class="row-2">
                <div class="box-2" @click="setVal(0)" id="c0" ></div>
                <div class="box-2" @click="setVal(1)" id="c1"></div>
                <div class="box-2" @click="setVal(2)" id="c2"></div>
            </div>
            <div class="row-2">
                <div class="box-2" @click="setVal(3)" id="c3"></div>
                <div class="box-2" @click="setVal(4)" id="c4"></div>
                <div class="box-2" @click="setVal(5)" id="c5"></div>
            </div>
            <div class="row-2">
                <div class="box-2" @click="setVal(6)" id="c6"></div>
                <div class="box-2" @click="setVal(7)" id="c7"></div> 
                <div class="box-2" @click="setVal(8)" id="c8"></div>
            </div>
            <div style="color:red; text-align: center" class="message" id="msg">{{message}}</div>
        </div>
    
        
    </div>
    
</body>
    </div>
</template>

<script>

export default {
    name: 'Home',
    data(){
        return{
           cells : [
                        null,
                        null,
                        null,
                        null,
                        null,
                        null,
                        null,
                        null,
                        null
                    ],
           value:'',
           color:'',
           message:'',
           r:'',
           moves: 9  
        }
    },
    methods:{
        changeVal(val,col){

            this.r = "b" + val
            this.value = val
            this.color = col        
        },

        async setVal(id){

             if(this.value === ''){
               this.message = 'No number chosed!'
               return

             }
             
             

              const cellName = "c"+ id
            
              const cell = document.getElementById(cellName)
           
           
            if(this.cells[id] == null && this.value !== ''){

                 this.message = ''
                 this.cells[id] = this.value
                 cell.style.background = this.color.toString()
                 cell.innerHTML = this.value
                 this.moves = this.moves - 1;
                 this.value = '';
                 this.color = ''
                
                 const r = this.r
                 const cel = document.getElementById(r)
                 cel.parentNode.removeChild(cel)

                this.checkGame()
            }

            

        },
        checkGame(){
           
             const cells = this.cells
             if(this.moves === 0){

                const moves = document.getElementById('moves')
                moves.style.color = 'red' 

                if(cells[1]-cells[0] === 1 && cells[2]-cells[1] === 1){
                   if(cells[5]-cells[2] ===1 && cells[4]-cells[5]=== 1){
                        if(cells[3]-cells[4] ===1 && cells[6]-cells[3]=== 1){
                            if(cells[7]-cells[6] ===1 && cells[8]-cells[7]=== 1){

                                 const row = document.getElementById('row1')
                                row.innerHTML = "<h1  style = 'color:#545454' >Won</h1>"
                                return

                            }
                        }
                    }
                }

                if(cells[8]-cells[7] === 1 && cells[7]-cells[6] ===1){
                   if(cells[6]-cells[3]===1 && cells[3] - cells[0]===1){
                       if(cells[0]-cells[1]===1 && cells[1]-cells[5]===1 ){
                           if(cells[2]-cells[4] === 1){

                                const row = document.getElementById('row1')
                                row.innerHTML = "<h1  style = 'color:#545454' >Won</h1>"
                                return

                           }
                       }
                   }
                }
                
                if(cells[2]-cells[5] === 1 && cells[5]-cells[8] === 1){
                    if(cells[8]-cells[7] === 1 && cells[7]-cells[4] === 1){
                        if(cells[4]-cells[1] === 1 && cells[1]-cells[0] === 1){
                           if(cells[0]-cells[3] === 1){

                                const row = document.getElementById('row1')
                                row.innerHTML = "<h1  style = 'color:#545454' >Won</h1>"
                                return

                           }
                        }
                    }
                }

                if(cells[3]-cells[0] === 1 && cells[6]-cells[3] === 1){
                    if(cells[7]-cells[6] === 1 && cells[4]-cells[7] === 1){
                        if(cells[1]-cells[4] === 1 && cells[2]-cells[1] === 1){
                            if(cells[1]-cells[4] === 1 && cells[2]-cells[1] === 1){

                                const row = document.getElementById('row1')
                                row.innerHTML = "<h1  style = 'color:#545454' >Won</h1>"
                                return

                            }
                        }
                    }
                }

                if(cells[5]-cells[2] === 1 && cells[8]-cells[5] === 1){
                    if(cells[7]-cells[8] === 1 && cells[4]-cells[7] === 1){
                        if(cells[1]-cells[4] === 1 && cells[0]-cells[1] === 1){
                            if(cells[3]-cells[0] === 1 && cells[6]-cells[3] === 1){

                                const row = document.getElementById('row1')
                                row.innerHTML = "<h1  style = 'color:#545454' >Won</h1>"
                                return

                            }
                        }
                    }
                }

                if(cells[5]-cells[8] === 1 && cells[2]-cells[5] === 1){
                    if(cells[1]-cells[2] === 1 && cells[4]-cells[1] === 1){
                       if(cells[7]-cells[4] === 1 && cells[6]-cells[7] === 1){
                           if(cells[3]-cells[6] === 1 && cells[0]-cells[3] === 1){

                                const row = document.getElementById('row1')
                                row.innerHTML = "<h1  style = 'color:#545454' >Won</h1>"
                                return

                           }
                       }
                    }
                }
                
                if(cells[7]-cells[8] === 1 && cells[6]-cells[7] === 1){
                    if(cells[3]-cells[6] === 1 && cells[4]-cells[3] === 1){
                        if(cells[5]-cells[4] === 1 && cells[2]-cells[5] === 1){
                            if(cells[1]-cells[2] === 1 && cells[0]-cells[1] === 1){
                                const row = document.getElementById('row1')
                                row.innerHTML = "<h1  style = 'color:#545454' >Won</h1>"
                                return
                            }
                        }
                    }   
                }



                     const row = document.getElementById('row1')
                     row.innerHTML = "<h1  style = 'color:#f11e1e' >Loss</h1>"
             }
             
                
        },
        replay(){
             location.reload();
        }
    }
}

</script>

<style>
body{
     padding: 0;
    margin: 0;  
}
header{
    display: flex;
    justify-content: center;
    height: 70px;
    padding: 15px;
    box-sizing: border-box;
}
header span{
    font-size: 20px;
    
}
.btn{
    border-radius: 4px;
    border: none;
    height: 28px;
    background-color: #007bff;
    cursor: pointer;
    margin-left: 25%;
    color: cornsilk;
    font-size: .875rem;
    
}
.container{
    display: flex;
        
}

.row-1{
    display: flex;
    margin-top: 10px
   
}
.row-2{
    display: flex;
    justify-content: center;
    padding: 10px;
   
}
.box-1{
    height: 55px;
    width: 53px;
    margin: 0 10px;
    border-radius: 2px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 30px;
    cursor: pointer;
}
.box-2{
    box-shadow: 0 2px 8px rgb(33 33 33 / 40%);
    height: 100px;
    width: 100px;
    text-align: center;
    border-radius: 4px;
    margin: 0 15px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 40px;
    cursor: pointer;
    transition: all .4s ease-in;
}
.box-2:hover{
    border: 3px dotted grey;
}
.left{
    height: 150px;
    width: 30%;
    margin-left: 25%;
}
.right{
    height: 500px;
    margin-top: 20px;
    
}
.txt{
    margin-left: 10px;
}

@media(max-width:1000px) {
    .container{
        display: flex;
        flex-direction: column;
    }
    .row-1{
    display: flex;
    justify-content: center;
    margin-top: 10px;
  
   }
   .left{ 
       margin-left: 12%;
       width: 80%;
   }
   .txt{
       text-align: center;
   }
}
</style>