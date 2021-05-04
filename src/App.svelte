<script>
  const ppcomision= 0.30;

  //env module
  //valor input enviar
  let envvalue ="";
  $: envvaluenum= Number(envvalue);
  //porcentaje comision
  let envcomisionpercent;
  //cuanto recibe
  let totalrecibido;

  //recibir module
  let recvalue ="";
  $: recvaluenum= Number(recvalue);
  let reccomisionpercent;
  let recenv;


  function handleInput(_event) {
    // Delay actual processing to the next
    // event cycle when the two-way binding
    // has synchronized `input.value`
    // to the component top level `value`.
    //
    self.setTimeout(handleInputDelayed());
  }

  function handleInputDelayed() {
    return () => {
      // Given that `value` has
      // now been synchronized with the
      // potentially invalid `input.value`
      // reactivity should easily detect
      // when we CHANGE it back to the
      // previous valid version
      //env
      envvalue = sanitize(envvalue);
      envcomisionpercent = comision(envvalue);
      totalrecibido = recibido(envcomisionpercent,  envvalue);
//rec
      recvalue = sanitize(recvalue);
      reccomisionpercent = reccomision( recenv, recvaluenum);
      recenv = reciben(recvalue);
    };
  }
  function sanitize(string) {
    let result = "";
    for (const c of string) {
      if ((c >= "0" && c <= "9") || c === ".") {
        result += c;
      } else {
        alert("just num pls");
      }
    }
    return result;
  }

//comision percent env
function comision(){
 let result=(envvalue*5.4)/100 +ppcomision;
 return Number(result.toFixed(2));
};
// recibido env
function recibido(){
 let result=Number(envvalue)-Number(envcomisionpercent);
 return result.toFixed(2);
};

//rec
function reccomision(){
  let result= reciben() - recvaluenum ;
 return Number(result.toFixed(2));
};

// recibido env
function reciben(){
 let result=(recvaluenum + ppcomision)/0.946;
 return Number(result.toFixed(2));
};

//toggle
let enviar;

let recibir;

 function showenv(){
  enviar.style.display='Block';
  recibir.style.display='none';
  //console.log(enviar.style.display='none');
 /* if (enviar.style.display==='' & recibir.style.display==='block' ) {
    enviar.style.display="block";
    recibir.style.display="";
} else if (enviar.style.display==='block' & recibir.style.display===''){
  enviar.style.display="";
    recibir.style.display="block";
}
   */

  
 }

 function showrec(){
  enviar.style.display='none';
  recibir.style.display='Block';
 }
</script>

<main>
  <div class="container">
    <div class="options">
      
      <button on:click="{showenv}"
        ><i class="fas fa-hand-holding-usd" style="font-size:4rem;" /><br /> Enviar
      </button>
      <button on:click="{showrec}"
        ><i class="fas fa-donate" style="font-size:4rem;" /><br
        />Recibir</button
      >
    </div>
    <div class="inputs"  bind:this={enviar}  >
      <span>Si se envian usd:</span>
      <input type="text" placeholder="0" 	on:input={handleInput} 
      bind:value={envvalue} />
      <span>La comision es de:</span>
      <input type="text" disabled placeholder={envcomisionpercent} id="comision" />
      <span>Se reciben usd:</span>
      <input type="text" placeholder={totalrecibido} disabled  id="recitotal"/>
    </div>

    <div class="inputs" bind:this={recibir} id="recibir">
      <span>Para recibir usd:</span>
      <input type="text" placeholder="0" 	on:input={handleInput} 
      bind:value={recvalue} />
      <span>La comision es de:</span>
      <input type="text" disabled placeholder={reccomisionpercent}  />
      <span>Hay que enviar usd:</span>
      <input type="text" placeholder={recenv} disabled  />
    </div>
  </div>
</main>

<style>
  main {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    max-width: 100vw;
  }

  .container {
    background-color: rgb(55, 119, 156);
    width: 25rem;
    height: auto;
    border-radius: 8%;
    box-shadow: 0px 0px 10px 6px darkslategray;
  }
  .options {
    display: flex;
    flex-direction: row;
    flex: 1;
    justify-content: center;
    align-content: center;
    padding: 50px;
  }
  .options button {
    align-items: center;
    min-height: 120px;
    min-width: 120px;
    margin: 4%;
    box-shadow: 0px 0px 12px 8px darkslategray;
    border-radius: 100%;
  }
  input {
    display: block;
    width: 70%;
    position: relative;
    margin: 2% 50%;
    transform: translateX(-50%);
    text-align: end;
    font-size: 1.4rem;
  }
  .inputs {
    display:none;
    position: relative;
    height: 100%;
    bottom: 50px;
    text-align: center;
    
  }

  #recitotal{
    text-align:center;
  font-size: 1.8rem;
  }




  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
