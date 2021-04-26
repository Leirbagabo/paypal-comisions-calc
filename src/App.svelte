<script>
  let name;
</script>

<main>
  <div class="container">
    <div class="options">
      <button><i class="fas fa-hand-holding-usd" style="font-size:4rem;"></i><br> Enviar </button>
      <button><i class="fas fa-piggy-bank" style="font-size:4rem;"></i><br>Recibir</button>
    </div>
    <div class="inputs">
      <span>Si se envian usd:</span>
      <input type="text" placeholder="0" />
      <span>La comision es de:</span>
      <input type="text" disabled />
      <span>Se reciben usd:</span>
      <input type="text" disabled />
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
    width: 30vw;
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
	padding:50px;
	
  }
  .options button {
    align-items: center;
	height:150px;
	width:150px;
	margin:2%;
  box-shadow: 0px 0px 12px 8px darkslategray;
  border-radius:100%;

  }
  input {
    display: block;
    width: 70%;
    position: relative;
    margin: 2% 50%;
    transform: translateX(-50%);
    text-align:end;
    font-size: 1.4rem;
  }
  .inputs {
    position: relative;
    height: 100%;
    bottom: 50px;
    text-align:center;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
