<script>
  const ppcomision= 0.30;
  //valor input
  let value ="";
  //valor convertido a numero con re-render on input
  $:  valuenum= Number(value);
  //porcentaje comision
  let comisionpercent;
  $ valuenum;
  //cuanto recibe
  let totalrecibido;

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
      //
      value = sanitize(value);
      comisionpercent = comision(valuenum);
      totalrecibido = recibido(comisionpercent);
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

//$:console.log(valuenum);
function comision(){
 let result=(valuenum*5.4)/100 +ppcomision;;
 return result.toFixed(2);
};

function recibido(){
 let result=valuenum+comisionpercent;
 return result.toFixed(2);
};
  
</script>

<main>
  <div class="container">
    <div class="options">
      <button
        ><i class="fas fa-hand-holding-usd" style="font-size:4rem;" /><br /> Enviar
      </button>
      <button
        ><i class="fas fa-donate" style="font-size:4rem;" /><br
        />Recibir</button
      >
    </div>
    <div class="inputs">
      <span>Si se envian usd:</span>
      <input type="text" placeholder="0" 	on:input={handleInput} 
      bind:value={value} />
      <span>La comision es de:</span>
      <input type="text" disabled placeholder={comisionpercent} id="comision" />
      <span>Se reciben usd:</span>
      <input type="text" placeholder={totalrecibido} disabled />
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
    position: relative;
    height: 100%;
    bottom: 50px;
    text-align: center;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
