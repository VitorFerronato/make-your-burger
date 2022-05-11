<template>
  <div>
    <Message :msg='msg' v-show='msg' />
    <div id="burger-container">
      <form @submit='createBurger'>
        <div class="input-container">
          <label for="nome">Nome do cliente</label>
          <input
            type="text"
            id="nome"
            name="nome"
            v-model="nome"
            placeholder="Digite o seu nome"
          />
        </div>

        <div class="input-container">
          <label for="pao">Escolha o pão:</label>
          <select name="pao" id="pao" v-model="pao">
            <option value="">Selecione o seu pão</option>
            <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
              {{ pao.tipo }}
            </option>
          </select>
        </div>

        <div class="input-container">
          <label for="carne">Escolha a carne:</label>
          <select name="carne" id="carne" v-model="carne">
            <option value="">Selecione o tipo de carne</option>
            <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
              {{ carne.tipo }}
            </option>
          </select>
        </div>

        <div id="opcionais-container" class="input-container">
          <label id="opcionais-title" for="opcionais"
            >Selecione os opcionais:</label
          >

          <div class="checkbox-content">
            <div
              class="checkbox-container"
              v-for="opcional in opcionaisdata"
              :key="opcional.id"
            >
              <input
                type="checkbox"
                name="opcionais"
                v-model="opcionais"
                :value="opcional.tipo"
              />
              <span>{{ opcional.tipo }}</span>
            </div>
          </div>
        </div>

        <div class="input-container">
          <input class="submit-btn" type="submit" value="Criar meu Burger!" />
        </div>
      </form>
    </div>
    
  </div>
</template>

<script>
import Message from './Message.vue';
export default {
  components: { Message },
  name: "Form",

  data() {
    return {
      // Dados que vem do servidor para preencher os inputs
      paes: null,
      carnes: null,
      opcionaisdata: null,
      // Dados do cliente após escolha
      nome: null,
      pao: null,
      carne: null,
      opcionais: [],
      msg: null,
    };
  },

  methods: {
    async getIngredientes() {
      // Espera pegar os dados dessa rota para passar para a próxima tarefa
      const req = await fetch("http://localhost:3000/ingredientes");

      // Espera pegar os dados da url e transforma em JSON
      const data = await req.json();

      // Atribuindo os dados do json as váriaveis do data
      this.paes = data.paes;
      this.carnes = data.carnes;
      this.opcionaisdata = data.opcionais;
    },

    // Essa função recebe o próprio evento de clique para previnir o reload da página, que é padrão do submit do form
    async createBurger(e) { 
      e.preventDefault() 

      // Atribuindo os valores dos inputs em variaveis para serem cadastradas no banco de dados no htpps://localhost:3000/burgers
      const data = { 
        nome: this.nome,
        pao: this.pao,
        carne: this.carne,
        opcionais: Array.from(this.opcionais),
        status: 'Solicitado'
      }

      // Mudando os dados de data para formato de texto
      const dataJson = JSON.stringify(data)
      
      // Enviando o pedido dos burgers para o banco de dados
      const req = await fetch('http://localhost:3000/burgers',{
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        body: dataJson
      })

      // Retornando os valores em formato de json object
      const res = await req.json()

      // Mensagem do sistema
      this.msg = `Pedido N ${res.id} realizado com sucesso`
      
      // Limpar mensagem do sistema
      setTimeout(() => this.msg = '', 2000)

      // Limpar os campos
      this.nome = ''
      this.carne = ''
      this.pao = ''
      this.opcionais = ''

    }
  },

  mounted() {
    this.getIngredientes();
  },
};
</script>

<style scoped>

#burger-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-left: 10rem;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

label {
  font-weight: bold;
  margin-bottom: 15px;
  color: var(--dark-color);
  padding: 5px 10px;
  border-left: 3px solid var(--first-color);
}

input,
select {
  padding: 5px 10px;
  width: 300px;
}

.checkbox-content {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

#opcionais-title {
  width: 100%;
}

.checkbox-container {
  display: flex;
  align-items: center;
  width: 50%;
  margin-bottom: 20px;
}

.checkbox-container span,
.checkbox-container input {
  width: auto;
}

.checkbox-container span {
  margin-left: 6px;
  font-weight: bold;
}

.submit-btn {
  background-color: var(--dark-color);
  color: var(--first-color);
  font-weight: bold;
  border: 2px solid var(--dark-color);
  padding: 10px;
  font-size: 16px;
  margin:  1rem auto;
  cursor: pointer;
  transition: 0.5s;
  transform: translateX(-5rem);
  border-radius: 5px;
}

.submit-btn:hover {
  background-color: transparent;
  color: var(--dark-color);
}
</style>