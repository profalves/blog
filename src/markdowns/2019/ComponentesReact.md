# 5 coisas essenciais ao aprender React

![React Logo](https://miro.medium.com/max/3200/1*OvYjQmX9G7QXZkMYQE-wpQ.jpeg)

Ao longo de minha experiência com React, sempre pensei em maneiras de como melhorar cada vez mais o meu código. Mas como eu fui autodidata nesse assunto, iniciei estudando materiais aleatórios, uns mais básicos porém outros mais avançados, o que não tornou meus estudos tão fácil.

Inspirado em como eu vejo claramente coisas que utilizo atualmente, farei uma abordagem na forma de como gostaria de ter aprendido se tivesse começando a aprender React hoje, ou até mesmo para quem está iniciando os seus estudos com essa biblioteca.


## 1. Componentes

> *"Tudo em React é componente"*

Acho que essa foi a citação que eu mais encontrei em materiais no início de meus estudos com *reactjs*. E verdadeiramente a principal diferença do React e entre outras bibliotecas semelhantes como *Polymer* ou *Angular* por exemplo, está em sua habilidade de separar as funcionalidades da aplicação por componentização e gerenciamento de estado... Calma, que logo entenderá tudo isso a partir de agora:

##### *Mas o que são componentes?*

> * "Componentes são conjuntos isolados de lógica (Javascript), visualização (JSX/HTML) e estilização (CSS)."*


```javascript
import React from "react";

export default function Button() {
  return (
    <button onClick={() => alert("Clicked")}>Click me</button>
  );
}
```

Acima está um exemplo de um componente React. Em resumo, os componentes em React nos deixam mais produtivos. Com eles temos um reaproveitamento de código maior (devido a possibilidade de reusar os componentes) e uma performace otimizada graças ao seu *VirtualDOM*, por renderizar somente os componentes que tiveram alterações em seu **estado**, ao invés de ter que esperar a renderização de todos os compoenentes em tela.

## 2. Estado de um componente (State)

> *"Componentes reagem ao estado"*

Essa para mim, é a frase que mais dá sentido ao nome **React**.

O estado (*ou state*) da sua aplicação, pode ser definido como: o lugar onde os dados chegam e se transformam ao longo do tempo.

Sendo assim, os componentes React podem ser divididos em duas categorias: *Stateless* (sem estado) e *Stateful* (com estado).

Os componentes do tipo *Stateless*, tem como característica somente a apresentação dos dados, portanto não tem estado.

Eles podem ser escritos como uma simples função:

```jsx
import React from 'react';

export default function Welcome() {
  return (
    <h1>Hello World</h1>  
  );
}
```
O ideal é escrever o máximo possível de componentes dessa categoria. Eles são mais fáceis de desenvolver, manter e testar.

Já os componentes do tipo *Stateful*, além da apresentação dos dados, tem que lidar também com algum tipo de lógica, ou transformação de dados. Por isso necessitam de estado.


```jsx
import React from 'react';

export default class Welcome extends React.Component {
  constructor(props) {
    super(props);
    this.state = { name: 'World' };
  }
  
  render() {
    return (
      <h1>Hello {this.state.name}</h1>
    );
  }
}
```

Os dois exemplos mostrados acima tem exatamente o mesmo resultado final. A única diferença é que o primeiro deles não usa o state do React, enquanto que o segundo usa.

## 3. Props

Agora falando em desenvolvimento de software de forma geral, passar parâmetros é extremamente comum. Com os componentes do React isso não poderia ser diferente. A diferença é que no React, usamos os *props* (*abreviação para properties*).

Assim como no HTML, podemos repassar propriedades nas notações dos nossos componentes e acessá-las de forma muito rápida. No exemplo abaixo, repassamos um título para cada post através do componente principal:

```jsx
// components/Lista.js

import React from 'react';
import Post from 'Post';

const App = () => {
  render() {
    return (
      <Post title="Aprendendo React" />
      <Post title="A RocketSeat é massa!" />
      <Post title="Não sei mais outro título" />
    );
  }
}
```

Agora em nosso componente de Post podemos acessar essa propriedade facilmente acessando a referência **this.props**:

```jsx
// components/Post.js

import React from 'react';

const App = () => { 
  render() {
    return <h1>{this.props.title}</h1>;
  }
}
```

Agora uma característica pouco transimitida para muitos iniciantes é que as props são **Read Only** (*Somente Leitura*).

Segundo a documentação oficial, independente de você declarar um componente como uma *função* ou como uma *classe*, ele nunca deve modificar seus próprios props. Considere essa função *sum*:

```javascript
function sum(a, b) {
  return a + b;
}
```
Tais funções são chamadas “puras” porque elas não tentam alterar suas entradas e sempre retornam o resultado utilizando as mesmas entradas, sem modificá-las em si.

Em contraste, essa função abaixo é "impura" porque altera diretamente a sua própria entrada:

```javascript
function withdraw(account, amount) {
  account.total -= amount;
}
```
Então fique atento, React é bastante flexível mas tem uma única regra estrita: **Todos os componentes React tem que agir como funções puras em relação ao seus props.**

Mas parece tão clichê falar sobre esses tópicos quando se está ensinando React para um iniciante, não é?

Claro que em qualquer lugar, seja em um curso, ou em qualquer maneira onde vá pesquisar para aprender React por conta própria (*a documentação se encaixa muito bem nesse contexto*), sempre irá começar por: *Componentes*, *Estados* e *Props*. 

E sem sombras de dúvidas, é realmente por onde é necessário começar a entender, mas algo que deveriam já falar desde o inicio é que há diferentes formas de declarar um componente e é isso que veremos agora:

## 4. Componente *Function* ou *Class*?

##### *Mas afinal, qual é a diferença?*

Na verdade, essa pergunta não é específica para o React, mas da linguagem JavaScript:

Antes do **ECMAScript 2015 (também chamado "ES6")**, não existia a utilização de <u>class</u> no JavaScript. Essa palavra-chave foi adicionada no ES6, permitindo definir classes. Mas na verdade não se trata de nada além de um *açúcar sintático* para a Function, como o exemplo abaixo mostrando uma saída do console:

```javascript
class Hello {}
Hello.constructor; // => ƒ Function() { [native code] }
```

Agora voltando para o React, com isso você pode definir um componente usando uma função ou uma classe.

##### Componente funcional sem estado

A maneira mais simples de definir um componente de React é usando uma função. Um componente definido dessa maneira não mantém o estado (*state*), nem contém métodos de ciclo de vida (agora usamos *hooks*). Segue o exemplo que é encontrado na [documentação](https://pt-br.reactjs.org/docs/components-and-props.html):

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

Essa função é um componente React válido porque aceita um único argumento de objeto “props” (que significa propriedades) com dados e retorna um elemento *JSX* (Uma espécie de XML para o Javascript). Nós chamamos esses componentes de “componentes de função” porque são literalmente funções JavaScript.

##### Componente de classe

Outra maneira, antes usada para construir um componente é usando uma classe de ES6. Segue um exemplo:

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

Os dois componentes acima são equivalentes ao ponto de vista do React.

Nas versões mais atuais do React, você encontrará os componentes sendo iniciados por uma **função**, ao invés de **classe** como nas versões anteriores, mesmo sendo *stateful*. Porém em muitas empresas que desenvolvem a um tempo com react, você com certeza encontrará muitos projetos com componentes sendo iniciados por classe. Essa mudança veio juntamente com os *Hooks*, que veremos agora:

## 5. Ciclo de vida da aplicação

Para que seja possível o desenvolvimento de componentes mais complexos, alguns métodos foram adicionados na API dos componentes React. 

Muito utilizado até um pouco tempo atrás e até hoje em projetos mais antigos, o Component Lifecycle (ciclo de vida dos componentes), são esses métodos, onde os desenvolvedores podem saber quando um componente vai ser criado, atualizado, destruído, etc.

![infografico lifecicle](https://cdn-images-1.medium.com/max/800/1*smGro1UuhyqopVT4aEsIrA.png)

Um exemplo de uso dos métodos de lifecycle, ao criar o contador de segundos abaixo:

```jsx
import React from 'react';

export default class Timer extends React.Component {
  constructor(props) {
    super(props);
    this.state = { elapsed: 0 };
    this.tick = this.tick.bind(this);
  }
  
  componentDidMount() {
    this.timer = setInterval(this.tick, 1000);
  }
  
  componentWillUnmount() {
    clearInterval(this.timer);
  }
  
  tick() {
    this.setState({ elapsed: this.state.elapsed + 1 });
  }
  
  render() {
    return <h1>{this.state.elapsed} seconds</h1>;
  }
}
```
Assim que o componente é montado (***componentDidMount***), nós iniciamos o setInterval que a cada 1000ms invocando a função *tick*. E quando o componente for destruído (***componentWillUnmount***) removemos o setInterval para que a função tick não continue sendo chamada desnecessariamente.

Porém se isso ficou um pouco abstrato para você não se preocupe, você nem precisará utilizá-los, pois os *Hooks* vieram para te ajudar!

![hooks](https://www.cronj.com/blog/wp-content/uploads/React-Hook.png)

Hooks são uma nova adição ao React 16.8. Eles permitem que você use o state e outros recursos do React sem escrever uma classe. 

Tenhamos como exemplo o código acima e em como o estado fora criado:

```jsx
import React from 'react';

export default class Timer extends React.Component {
  constructor(props) {
    super(props);
    this.state = { elapsed: 0 };
    this.tick = this.tick.bind(this);
  }
  ...
```
Agora utilizando um dos métodos do hook, chamado ***useState***:

```jsx
import React, { useState } from 'react';

function Timer() {
  const [elapsed, setElapsed] = useState(0);
  ...
```
Se valendo do *destructuring* do **ES6**, o mesmo estado fora declarado dentro de uma uma função, trazendo um código menos verboso ao criar o estado.

Este é o hook mais comum e mais utilizado para controlarmos alguma variável de estado. Para utilizar definimos:

```js
const [elapsed, setElapsed] = useState(0);
```

O primeiro valor *count* representa o valor do estado que será manipulado pela função *setCount* recebida através da desestruturação realizada no useState. O valor 0 repassado ao hook é o valor inicial do estado.

Agora em relação ao ciclo de vida digamos que os hooks não vieram substituir mas suprir uma das grandes deficiência dos components funcionais, que sempre foi lidar com chamadas à API, tarefas assíncronas, modificações na DOM, etc. Com o hook ***useEffect*** podemos operar *"efeitos colaterais"* mediante um estado durante a renderização do nosso componente.

Ainda baseado no exemplo acima, digamos que iremos realizar o mesmo parecido com o *componentDidMount*

```jsx
useEffect(() => {
  this.timer = setInterval(this.tick, 1000);
}, [elapsed])
```

Veja que o hook recebe como primeiro parâmetro uma função (assíncrona ou não) que é executada após inicialização e atualização do componente, mais ou menos o que temos com o **componentDidMount** e **componentDidUpdate** no *stateful component*.

O segundo parâmetro **[elapsed]** indica em quais situações esse effect deve executar, nesse caso ele só executará caso o valor de count alterar. Podemos também não repassar esse parâmetro e indicaremos ao hook que deve executar na inicialização e em todas atualizações do componente, independente de seus valores alterarem.

Outra dica é que você pode passar um array vazio [] ao hook como segundo parâmetro garantindo que o mesmo irá executar apenas uma vez na inicialização do componente (*isso se aproxima mais de um componentDidMount*)

Temos mais hooks para estudar, tais como o ***useContext*** (*que substitui a a Context API do React*), ***useReducer*** (*que trouxe junto com ele os boatos de que o Redux morreria*) e até mesmo o ***memo*** (*que possibilita a escolha de quem vai renderizar ou não mais de uma vez, travando e memorizando a primeira renderização do componente*), mas por agora os que citei acima são suficientes para dar uma idéia da solução trazida com os *Hooks*.

## Conclusão

Eu penso em como essa abordagem me ajudaria no inicio dos meus estudos em React. Claro que estou partindo do pressuposto que já entendam pelo menos o javascript e suas principais funcionalidades (*pois é inevitavelmente um pré-requisito*). 

Na minha opinião compreendendo claramente sobre componentes, state, props e a utilização dos hooks da qual citei acima, já teria uma base sólida para construir muitas aplicações, pois colocar a mão na massa vale bem mais do que qualquer aprofundamento teórico na maioria dos casos.

Se quer se profundar mais sobre este assunto e mergulhar no ecossistema React, pode se inscrever em nosso curso de [Javascript]()

