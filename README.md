# <center>VueJS 3</center>

---

### v-if e v-show
<p>o v-if funciona como condicao onde vc colocar em um componente por ex</p>

````vue
<TheHeader v-if="showHeader"/>

<script>
  export default {
    // data() onde fica as variaveis
    data(){
      return{
        showHeader: true
      }
    }
  }
</script>
````

````vue
<TheHeader v-if="accessLvl === 'admin'"/>

<script>
  export default {
    // data() onde fica as variaveis
    data(){
      return{
        showHeader: true,
        // isso fara com que somente o admin veja o conteudo
        accessLvl: 'admin',
      }
    }
  }
</script>
````
- nesse exemplo o componente TheHeader vai ser mostrado para o usuario,mas caso fosse falso ele ia ficar invisivel.

<p>A diferença entre o v-if e o v-show, é que o v-show voce pode ver o componente no inspecionar codigo, ja o v-if ele ja nao mostra.</p>

<br>

### v-for and v-bind

<p>O v-bind é uma diretiva no Vue.js que permite associar um valor dinâmico a um atributo de um elemento HTML.</p>

<p>a funcionalidade do v-for, funciona como qualquer outra linguagem de repeticao</p>

````vue

<template>
  <!-- o v-bind pode ser simplificado assim :key="" -->
  <div v-for="obj in todos"
       :key="obj.id">
    {{ obj.title }}
  </div>
  <!-- pegando o index com o v-for -->
  <div v-for="(obj, index) in todos"
    :key="obj.id">
    {{ index }} - {{ obj.title }}
  </div>
</template>

<script>
  export default {
    // data() onde fica as variaveis
    data(){
      return{
        todos:[
          {
            'userId' :1,
            'id':1,
            'title': 'title1',
            'completed':false
          },
          {
            'userId' :2,
            'id':2,
            'title': 'title2',
            'completed':true
          },
          {
            'userId' :3,
            'id':3,
            'title': 'title3',
            'completed':false
          }
        ]
      }
    }
  }
</script>
````

### class and styles dynamic

<p>como manipular class e styles com o vuejs3</p>

````vue
<template>
  <h1 :class="classVar">
    vuejs3
  </h1>
</template>

<script>

export default {
  name: 'app',
  data(){
    return{
      classVar: 'title',
    }
  }
}
</script>
<style>
  .title{
    font-size: 20px;
    color: blue;
  }
</style>
````

#### array|obj in class dynamic

````vue
<template>
  <!-- aqui como esta true, quer dizer que as propriedades do css, vai ser executada -->
  <h1 :class="{'title': true}">
    vuejs3
  </h1>
</template>

<script>

export default {
  name: 'app',
  data(){
    return{
      classVar: 'title',
    }
  }
}
</script>
<style>
  .title{
    font-size: 20px;
    color: blue;
  }
</style>
````

````vue
<template>
  <!-- aqui como esta true, quer dizer que as propriedades do css, vai ser executada -->
  <h1 :class="pClass">
    vuejs3
  </h1>
</template>

<script>

export default {
  name: 'app',
  data(){
    return{
      pClass: ['text',{'title': true}],
    }
  }
}
</script>
<style>
  .text{
    color: gray;
  }
  .title{
    font-size: 20px;
    color: blue;
  }
</style>
````

### css v-bind dynamic

````vue
<template>
  <!-- aqui como esta true, quer dizer que as propriedades do css, vai ser executada -->
  <h1 :style="styleClass">
    vuejs3
  </h1>
</template>

<script>

export default {
  name: 'app',
  data(){
    return{
      styleClass: {'color' : 'aqua', 'background-color': 'black'},
    }
  }
}
</script>

<style>
  .text{
    color: gray;
  }
  .title{
    font-size: 20px;
    color: blue;
  }
</style>
````

---

## directive v-model

<p>
O v-model é uma diretiva no Vue.js que permite criar facilmente a funcionalidade de dois sentidos de binding entre um input HTML e uma variável no seu componente Vue.js.

Isso pode parecer complicado, mas vamos explicar com um exemplo simples. Digamos que você tenha um input HTML em seu template Vue.js e queira permitir que o usuário digite um valor nesse input. Você poderia usar o v-bind para associar o valor atual da variável do seu componente ao valor do input.
</p>

````vue
<template>
  <input
      v-model="name"
      type="text">
  
  {{ name }}
  <!-- quando o usuario vai escrevendo  -->
  <!-- no input a variavel {{ name }} ja vai mostrando na tela oque foi escrito. -->
</template>

<script>
export default {
  data(){
    return{
      name: ''
    }
  }
}
</script>
````

- utilizando select com v-model

````vue
<template>
  <select v-model="sports">
    <option value="">Escolha</option>
    <option value="futebol">futebol</option>
    <option value="basquete">basquete</option>
    <option value="volei">volei</option>
  </select>
</template>

<script>
export default {
  data(){
    return{
      // caso a variavel esteja vazia ele ja vem marco com a opcao 'Escolha'
      sports: '',
    }
  }
}
</script>
````

- utilizando radio com v-model

````vue
<template>
  
  <input type="radio"
         value="sim"
         v-model="newsletter">
  
  <input type="radio"
         value="nao"
         v-model="newsletter">
  
</template>

<script>
export default {
  data(){
    return{
      // caso a variavel esteja vazia ele nao marca nenhuma'
      newsletter: '',
    }
  }
}
</script>
````

- utilizando checkbox com v-model

````vue
<template>
  
<div>
  <label>Contrato</label>
  <input type="checkbox"
         v-model="contract"> Aceita nosso termos... <br>
</div>
  
</template>

<script>
export default {
  data(){
    return{
      // caso a variavel esteja vazia ele nao marca nenhuma'
      contract: false,
    }
  }
}
</script>
````
---

<br>

## Events | v-on

- O v-on é uma diretiva do Vue.js que é usada para adicionar ouvintes de eventos em elementos HTML. Ele permite que você responda a eventos do usuário, como clique de mouse, pressionamento de tecla, passagem do mouse sobre um elemento, etc. Quando você usa o v-on, você está basicamente dizendo ao Vue.js que ele deve esperar um evento acontecer e, em seguida, executar uma função que você especificou


- @mouseover - este evento é executado quando o cursor do mouse passa por cima do objeto desejavel, e assim entao ele se ativa e realiza a tarefa


- modificadores eventos - ele pode alterar o comportamento do evento, como o once que faz ele executar somente uma vez
````vue
<template>
  <div>
  <!-- o v-on vai ser executado quando houver um click no button   -->
  <!--  o v-on:click vai receber uma funcao/metodos  -->
  <!--  uma forma facil de simplificar o v-on é @click  -->
    ex1:<button v-on:click="onClick">Enviar</button>
    ex2:<button @click.once="onClick">Enviar</button>
  </div>
  
    <div @mouseover="onMouseover">
    Mouse Over
  </div>
</template>

<script>
  export default {
    data(){
      return{
        
      }
    },
    // o $evt mostra todas as informações do evento executado
    methods:{
      onClick($evt){
        console.log('click',$evt);
      },
      onMouseover(){
        console.log('onMouseover')
      },
    }
  }
</script>
````

### form with events

````vue
<template>
  <!-- o .stop faz com que ele nao siga para o site desejavel -->
  <form action="http://google.com"
        @submit.stop="onSubmit">
    
  </form>
  
  <button type="submit">Enviar</button>
</template>

<script>
  export default {
    data(){
      
    },
    methods:{
      onSubmit($evt){
        console.log('submit',$evt);
      }
    }
  }
</script>
````

---

<br>

## proprietary computed

<p>
O computed é uma propriedade do Vue.js que permite que você crie propriedades computadas a partir de outras propriedades ou dados da sua aplicação. É como se você criasse uma "variável" que é calculada automaticamente com base em outras variáveis que você já definiu.

Por exemplo, imagine que você tenha dois dados na sua aplicação, x e y, e que você queira calcular a soma desses dois valores e exibi-los na tela. Com o computed, você pode fazer isso de forma muito fácil e elegante, criando uma propriedade calculada que irá atualizar automaticamente sempre que x ou y forem atualizados.
</p>

````vue

<template>
  {{ fullName }}
</template>

<script>

export default {
  data() {
    return{
      user:{
        first_name: 'felipe',
        last_name: 'mateus',
      }
    }
  },
  computed: {
    // essa funcao so recomputa quando os valores forem alterados
    fullName() {
      return `${this.user.first_name} ${this.user.last_name} `
    }
  }
}
</script>
````

- outro exemplo
````vue
 <template>
  <!-- todos incompletas -->
  <h1>todos em aberto</h1>
  
  <div v-for="todo in uncompletedTodos"
  :key="todo.id">
    {{ todo.title }} 
    <span>{{ todo.completed }}</span>
  </div>
  
  
  <!-- todos completas -->
  <h1>Todos completadas</h1>
  
  <div v-for="todo in completedTodos"
       :key="todo.id">
    {{ todo.title }} 
    <span>{{ todo.completed }}</span>
    
  </div>
  
  <!-- todas as todos -->
  <h1>Todas as todos</h1>
  
  <div v-for="todo in todos"
       :key="todo.id">
  <!--  o v-model no checkbox pode fazer uma reatividade que altera os valores assim podendo modificar entre false e true no exemplo que estamos usando  -->
  <!--  fazendo alterar uma das 2 variaveis no computed assim alterando o estado da mesma  -->
    <input type="checkbox"
    v-model="todo.completed">
    
    {{ todo.title }}
    
  </div>
  
</template>

<script>

export default {
  data() {
    return{
      todos:[
        {
          'userId' :1,
          'id':1,
          'title': 'title1',
          'completed':false
        },
        {
          'userId' :2,
          'id':2,
          'title': 'title2',
          'completed':true
        },
        {
          'userId' :3,
          'id':3,
          'title': 'title3',
          'completed':false
        }
      ]
    }
  },
  computed: {
    uncompletedTodos(){
      return this.todos.filter(todo => !todo.completed)
    },
    completedTodos(){
      return this.todos.filter(todo => todo.completed)
    }
  }
}
</script>
````

## watch in vuejs 3

<p>
O watch em Vue.js é como um observador que monitora uma propriedade ou um conjunto de propriedades de um componente Vue.js. Quando o valor da propriedade monitorada é alterado, a função de callback do watch é acionada automaticamente. Basicamente, é uma forma de reagir a mudanças em uma propriedade e executar uma ação específica em resposta.

Por exemplo, se quisermos executar uma ação específica sempre que a propriedade username de um componente Vue.js for alterada, podemos usar o watch para monitorar essa propriedade e executar a ação desejada quando ela for alterada.
</p>

````vue
<template>
  <div>
    <input type="text"
           v-model="name">
    {{ name }}
  </div>
</template>

<script>
  export default {
    name: 'app',
    data(){
      return{
        name: ''
      }
    },
    computed:{
      
    },
    watch:{
      // aki onde fazemos nosso ajax(enviar/pegar dados do backend)
      // aki recebemos o novo valor e o velho valor, nessa funcao
      name(newValue,oldValue){
        console.log(newValue,oldValue);
      
        // é aconselhável separar a logica e a regra de negocio entre methods e watch
        this.saveUserName();
      
        // vai executar se o nome for maior ou igual a 3
        if (newValue.length >=3)
        {
          this.saveUserName();
        }
      }
    },
    methods:{
      // a funcao do watch(name) é executada e chega nos metodos na funcao que executa o newUserName()
      saveUserName(){
        console.log(this.name)
      }
    }
  }
</script>
````

- utilizando select com watch

````vue
<template>
  <div>
    <input type="text"
           v-model="name">
    {{ name }}
  </div>

  <select v-model="pageCount">
    <option value="5">5</option>
    <option value="10">10</option>
  </select>
  
  {{ pageCount }}
  
</template>

<script>
  export default {
    name: 'app',
    data(){
      return{
        pageCount: 5
      }
    },
    computed:{
      
    },
    watch:{
        pageCount(){
        this.changePage();
      }
    },
    methods:{
      // a funcao do watch(name) é executada e chega nos metodos na funcao que executa o newUserName()
      changePage(){
        console.log('ajax changePage')
      }
    }
  }
</script>
````
 <br>

#### Handler

<p>
"Handle" é um termo que pode ser usado em programação para se referir a um método, função ou objeto que é usado para lidar com alguma ação ou evento específico. Em outras palavras, é um bloco de código que é executado quando ocorre um determinado evento ou ação.

Por exemplo, em uma aplicação de formulário, o botão "Enviar" pode ter um "handle" atribuído a ele que dispara uma ação quando o botão é clicado. Esse "handle" pode ser uma função que valida os campos do formulário, envia os dados para um servidor ou exibe uma mensagem de confirmação.

Em resumo, um "handle" é uma forma de responder a eventos ou ações em um programa de computador. É um bloco de código que é executado em resposta a um evento específico, como um clique de mouse ou um toque na tela, por exemplo.
</p>

#### utilizando watch com obj

````vue
<template>
  <div>
    <input v-model="user.first_name" type="text">
    <br>
    <input v-model="user.last_name" type="text">
  </div>
</template>
<script>
  export default {
    data(){
      return{
        user:{
          first_name: '',
          last_name: ''
        }
      }
    },
    watch:{
      // handler funciona quando o user se alterar ele vai se executar
      user:{
        handler(){
          console.log('alterado');
        },
        // e o deep quando qualquer coisa deste objeto se alterar ele vai disparar o handler
        deep:true
      }
    }
  }
</script>
````

---

### component lifecycle vuejs

<p>
O ciclo de vida em Vue.js é um conjunto de etapas que um componente passa desde que é criado até que é destruído. É como se fosse um caminho que o componente segue, e em cada etapa desse caminho é possível executar ações específicas.

O ciclo de vida começa quando um componente é criado, e nesse momento é possível executar ações de inicialização, como definir o valor de variáveis ou fazer chamadas a APIs externas para buscar dados. Depois disso, o componente é montado na página e é possível interagir com ele.

Quando o componente é atualizado, ou seja, quando ocorrem mudanças nas propriedades ou no estado interno do componente, é possível executar ações específicas nesse momento. Além disso, também é possível monitorar quando o componente é destruído, para que ações de limpeza possam ser executadas, como liberar recursos que foram alocados.

O ciclo de vida é composto por várias etapas, como "beforeCreate", "created", "beforeMount", "mounted", "beforeUpdate", "updated", "beforeUnmount" e "unmounted". Em cada uma dessas etapas é possível executar ações específicas. O uso correto do ciclo de vida pode ajudar a otimizar a performance do componente e garantir um comportamento correto e consistente.
</p>

- exemplo:
````vue
<template>
  <div>
    <ul>
      <li v-for="post in posts" :key="post.id">{{ post.title }}</li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'MyComponent',
  data() {
    return {
      posts: [],
    };
  },
  async created() {
    try {
      const response = await axios.get('https://jsonplaceholder.typicode.com/posts');
      this.posts = response.data;
    } catch (error) {
      console.error(error);
    }
  },
};
</script>
````
- exemplo 2:
````vue
<template>
  <div>
    <h1>Hello World</h1>
    {{ name }}
  </div>
</template>
<script>
  export default {
    name: 'App',
    data(){
      return{
        name: 'felipe'
      }
    },
  // Criação
    // Preparar o componente
    // Ajax, Inicializar algumas variaveis
    // Não tem acesso ao template(DOM)
  // Montagem
    // Inicializar um lib externa (new lib())
    // Precisa de acesso ao template(DOM)
    //Tem acesso ao template(dom)
  // Atualização
    //Debug
    //Update
  // Desmontagem   
    //Remover tudo o que for necessario (li->destroy())
    //para liberar memoria
    
  // HOOKS
    beforeCreate(){
      console.log('DOM:', $el);
      console.log(this.name,'beforeCreate');
    },
    created()
    {
      console.log('DOM:', $el);
      console.log(this.name,'created');
    },
    beforeMounted(){
      console.log('DOM:', $el);
      console.log(this.name,'beforeMounted');
    },
    mounted(){
      console.log('DOM:', $el);
      console.log(this.name,'mounted');
    },
  }
</script>
````

### beforeUnmount | unmounted
<p>
Um exemplo de como funciona o beforeUnmount e o unmounted.
</p>

````vue
<template>
  <div v-if="showDiv">
    <h1>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aperiam earum eligendi</h1>
  </div>
  
  <button @click="showDiv = !showDiv">Toggle</button>
</template>
<script>
  export default {
    name: 'App',
    data(){
      return{
        showDiv: true
      }
    },
    beforeUnmount(){
      console.log('beforeUnmount');
    },
    unmounted(){
      console.log('unmounted');
    }
  }
</script>
````

### beforeUpdate | updated
<p>
Um exemplo de como funciona o beforeUpdate e o updated.
</p>

````vue
<template>
  <input v-model="name" 
         type="text">
</template>
<script>
  export default {
    name: 'App',
    data(){
      return{
        name: 'felipe'
      }
    },
    beforeUpdate(){
      console.log('beforeUpdate', this.name);
    },
    updated(){
      console.log('updated', this.name);
    }
  }
</script>
````

### capturar todos os comandos do vuejs em uma variavel global

<p>ele fica localizado no main.js</p>

````vue
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'

window.app = createApp(App).use(router).mount('#app')

````

--- 

<br>

## Components slots

<p>
Component slots em Vue.js é uma maneira de permitir que os usuários do componente insiram seu próprio conteúdo personalizado no componente.

Imagine que você tem um componente de caixa de diálogo que exibe informações para o usuário, mas você deseja permitir que o usuário adicione seus próprios botões personalizados para a caixa de diálogo. Com o componente slots, você pode definir um ponto de inserção em seu componente que permita que o usuário insira seu próprio conteúdo personalizado.

Por exemplo, imagine um componente de caixa de diálogo em que você defina um slot com o nome "footer". Em seguida, quando você usa o componente em seu aplicativo, pode adicionar seu próprio conteúdo personalizado dentro do slot "footer".
</p>


````vue
//App.vue
<template>
  <div>
    <TheHeader>
      
      <template v-slot:title>
        Title
      </template>
      
      <template v-slot:description>
       Description
      </template>
      
    </TheHeader>
  </div> 
</template>
<script>
  import TheHeader from '@/components/TheHeader';
  export default {
    name: 'App',
    components:{
      TheHeader,
    },
    data(){
      return{
        
      }
    }
  }
</script>
````

````vue
//TheHeader.vue
<template>
  <div>
    
    <h1 class="title">
      <slot name="title"/>
    </h1>
    
    <div class="description">
      <slot name="description"/>
    </div>
    
  </div>
</template>
<script>
  export default {
    name: 'TheHeader',
    mounted(){
      // this.slots, verifica o slots
      // $el verifica se foi montado a div com o $el
      console.log(this.$el)
    }
  }
</script>
````

---


## Scoped e global CSS

O Scoped CSS em VueJS é usado para aplicar estilos apenas no componente em que está sendo utilizado. Isso é feito usando o atributo "scoped" na tag `<style>` do componente. Dessa forma, os estilos definidos nesse componente não afetarão outros componentes no aplicativo.
<br><br>
Por outro lado, o Global CSS é usado para aplicar estilos que serão compartilhados em toda a aplicação. Esses estilos são definidos em um arquivo CSS global e podem ser acessados por todos os componentes.<br>
<br>
Resumindo, o Scoped CSS é usado para estilos específicos de um componente, enquanto o Global CSS é usado para estilos que devem ser aplicados em toda a aplicação.

````vue
<template>
  <div id="title">
    <h1>Lorem ipsum dolor sit amet.</h1>
  </div>
</template>
<!-- utilizando o scoped ele so vai atribuir o css para o componente -->
<style scoped>
  #title{
    background: red;
    padding: 10px;
  }
</style>
````

---

## props vuejs 3

<p>
O props é uma forma de passar informações de um componente pai para um componente filho no Vue.js.

Imagine que você tenha um componente pai que representa uma lista de tarefas, e dentro dele você tenha um componente filho que representa uma tarefa individual. Para exibir cada tarefa, você precisará passar algumas informações específicas, como o título e a descrição da tarefa, do componente pai para o componente filho. É aí que entra o props.

O componente filho define quais propriedades ele espera receber através do objeto props. O componente pai, por sua vez, pode passar informações específicas para o componente filho através dessas propriedades.
</p>

````vue
<!--Alert.vue Component-->
<template>
  
  <div :class="baseClass">
    {{ test }}
    <slot/>
  </div>
  
</template>
<script>
 export default {
   name: 'Alert',
   props: {
     variant:{
       variant:{
         type: String,
         default: ''
       },
       test:{
         type: String,
         default: 'test'
       },
     }
   },
   computed:{
     baseClass(){
       return [
           'alert',
           this.variant ? `alert-${this.variant}` : ''
       ];
     },
   }
 }
</script>
<style scoped>
  .alert{
    padding: 5px;
    border-radius: 6px;
    color: gray;
    background: #ddd;
  }

  .alert-success{
    background: #42b983;
    color: #fff;
  }

  .alert-danger{
    background: red;
    color: #fff;
  }
</style>
````

````vue
<!--App.vue Component-->
<template>
  <div>
    <Alert :variant="variant">
      {{ text }}
    </Alert>
  </div>
</template>
<script>
 import Alert from '@/components/Alert';
 export default {
   name: 'Alert',
   data(){
     return{
       variant: 'success',
       text: 'Seu formulario foi enviado com sucesso!!'
     }
   },
   components:{
     Alert
   },
 }
</script>
````

---

### method $emit em vuejs

<p>
O $emit é um método em Vue.js que permite que um componente filho envie um evento personalizado para o seu componente pai. Quando um evento é emitido por um componente filho, o componente pai pode ouvi-lo e reagir a ele.

Por exemplo, suponha que você tenha um componente filho que tenha um botão de "enviar". Quando o botão for clicado, você pode querer que o componente pai saiba que o botão foi clicado e talvez faça algo em resposta a esse evento. Para fazer isso, você pode usar o $emit no componente filho para emitir um evento personalizado chamado "enviar", e então ouvir esse evento no componente pai.

A sintaxe para emitir um evento personalizado é $emit('nomeDoEvento'), onde "nomeDoEvento" é o nome que você escolheu para o evento.
</p>

```vue
<!-- componente filho -->
<script>
export default {
  methods: {
    enviar() {
      this.$emit('enviar');
    }
  }
}
</script>

```

````vue
<!-- componente pai -->
<template>
  <div>
    <meu-componente-filho v-on:enviar="lidarComEnviar"></meu-componente-filho>
  </div>
</template>

<script>
import MeuComponenteFilho from './MeuComponenteFilho.vue';

export default {
  components: {
    MeuComponenteFilho
  },
  methods: {
    lidarComEnviar() {
      console.log('O botão de enviar foi clicado!');
    }
  }
}
</script>

````

### other ex:

````vue
<!-- App.vue component father -->
<template>
  <!-- evento personalizado criado (close) -->
  <Alert @close="onClose()"
         v-if="showAlert"/>
</template>
<script>
  import Alert from '@/components/Alert';
  export default {
    name: 'App',
    components:{
      Alert
    },
    data(){
      return{
        showAlert: true,
      }
    },
    methods:{
      onClose(){
        // fazendo isto ele remove da tela o componente alert
        this.showAlert = false;
        console.log('on close')
      }
    },
  }
</script>
````

````vue
<!-- Alert.vue component son -->
<template>
  <div>
    <button @click="onclick()">x</button>
  </div>
</template>
<script>
  export default {
    name: 'TheHeader',
    methods:{
      onClick(){
        // $emit vai enviar o evento para o pai
        this.$emit('close');//close é o nome do evento
        console.log('clickou');
      }
    }
  }
</script>
````

### how use $emit and props

````vue
<template>
  <div>
    <!--  do pai para o filho é props -->
    <PAI>
      <FILHO>
        <NETO></NETO>
        <!--  do neto para o filho é $emit = event  -->
      </FILHO>
    </PAI>
    
  </div>
</template>
````
