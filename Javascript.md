# `focusnetworks();`

Focusnetworks JavaScript code styleguide.

## Menu

* [Disclaimer](#disclaimer)
* [Ponto e vírgula](#ponto-e-vírgula)
* [Strict mode](#strict-mode)
* [Context e closures](#context-e-closures)
* [Variáveis](#variáveis)
  * [Definição de `var` simples](#definição-de-var-simples)
  * [Ordem](#ordem)
  * [Estilo](#estilo)
* [Objetos](#objetos)
  * [Sintaxe literal de objetos](#sintaxe-literal-de-objetos)
  * [Palavras reservadas](#palavras-reservadas)
  * [Chaves de objeto](#chaves-de-objeto)
* [Arrays](#arrays)
  * [Sintaxe literal de arrays](#sintaxe-literal-de-arrays)
  * [Adicionando itens](#adicionando-itens)
  * [Limpando array](#limpando-array)
  * [Conversão de array](#conversao-de-array)
* [Strings](#strings)
  * [Aspas](#aspas)
  * [Concatenação](#concatenação)
  * [Long strings](#long-strings)
  * [Conversão de strings](#conversão-de-strings)
* [Funções](#funções)
  * [Argumentos de funções](#argumentos-de-funções)
* [Convenções de nomenclatura](#convenções-de-nomenclatura)
  * [Nomenclatura de funções](#nomenclatura-de-funções)
  * [Nomenclatura de construtores](#nomenclatura-de-construtores)
  * [Nomenclatura de propriedades privadas](#nomenclatura-de-propriedades-privadas)
  * [Referenciando `this`](#referenciando-this)
  * [Nomenclatura de booleanos](#nomenclatura-de-booleanos)
  * [Nomenclatura de acessores](#nomenclatura-de-acessores)
  * [Nomenclatura de event handlers](#nomenclatura-de-event-handlers)
* [Propriedades](#propriedades)
* [Expressões condicionais e de igualdade](#expressões-condicionais-e-de-igualdade)
* [Blocos](#blocos)
* [Comentários](#Comentários)
* [Espaços em branco](#espaços-em-branco)
  * [Tabs](#tabs)
  * [EOF](#eof)
  * [Declaração de condições e loop](#declaração-de-condições-e-loop)
  * [Operadores](#operadores)
  * [Etapas de loops](#etapas-de-loops)
  * [Declaração de objetos](#declaração-de-objetos)
  * [Encadeamento](#encadeamento)
* [Verificação de tipo](#verificação-de-tipo)
  * [String](#string)
  * [Número](#número)
  * [Booleano](#booleano)
  * [Objeto](#Objeto)
  * [Array](#array)
  * [Node](#node)
  * [`null`](#null)
  * [`null` ou `undefined`](#null-ou-undefined)
  * [`undefined`](#undefined)
    * [Variável global](#variável-global)
    * [Variável local](#variável-local)
    * [Propriedade](#propriedade)
* [Melhores práticas](#melhores-práticas)
  * [jQuery](#jquery)
* [Links](#links)
  * [Styleguides](#styleguides)
  * [Artigos e posts](#artigos-e-posts)
  * [Ferramentas](#ferramentas)

## Disclaimer

Esse documento foi inspirado por [jQuery Style Guide](http://contribute.jquery.org/style-guide/js), [idiomatic.js](https://github.com/rwaldron/idiomatic.js) e [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript).

**[⬆ voltar ao menu](#menu)**

## Ponto e vírgulaa

* Sempre, por favor! [ASI](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Automatic_semicolon_insertion) é muito complicado, não confie nele.

```js
// Bad
(function() {
  var name = 'John'
  return name
})()

// Good
(function() {
  var name = 'John';
  return name;
})();
```

**[⬆ voltar ao menu](#menu)**

## Strict mode

* Você pode usar o strict mode. Basta estar atento para não usá-lo em modo global!

```js
// Bad
'use strict';

function doSomething() {
}

function doSomethingElse() {
}

// Good
function doSomething() {
  'use strict';
  // stuff
}

// Good
(function() {
  'use strict';

  function doSomething() {
  }

  function doSomethingElse() {
  }
})();
```

**[⬆ voltar ao menu](#menu)**

## Context e closures

* Sempre envolva seus módulos em closures (fechamentos) criando um contexto (context) único de execução. Jogar coisas no escopo global pode levar a todos os tipos de comportamentos estranhos.

```js
// Bad
function doAwesomeStuff() {
  $('.js-item').fadeIn();
}

function doEvenCoolerStuff() {
  $('.js-item').animate({top: 100}, 'fast');
}

// Good
(function($) {
  function doAwesomeStuff() {
    $('.js-item').fadeIn();
  }

  function doEvenCoolerStuff() {
    $('.js-item').animate({top: 100}, 'fast');
  }
})(jQuery);

// Good
var Module = (function() {
  function Module() {
    // magic happens here
  }

  return Module;
})();
```

**[⬆ voltar ao menu](#menu)**

## Variáveis

### Definição de `var` simples

* Use `var` simples na definição de variáveis.

```js
// Bad
var foo = 'Foo';
var bar = 'Bar';
var baz = 'Baz';

// Good
var foo = 'Foo',
    bar = 'Bar',
    baz = 'Baz';
```

### Ordem

* Variáveis sem valor de inicialização deve vir em primeiro lugar.

```js
// Bad
var name = 'John',
    surname = 'Doe',
    country,
    age = 42,
    email;

// Good
var country,
    email,
    name = 'John',
    surname = 'Doe',
    age = 42;
```

### Estilo

* Não siga o estilo "comma first"!

```js
// Bad (OMG, really bad!)
var once
  , upon
  , aTime;

// Good
var once,
    upon,
    aTime;

// Bad
var user = {
  name: 'John'
  , surname: 'Doe'
  , age: 42
};

// Good
var user = {
  name: 'John',
  surname: 'Doe',
  age: 42
};
```

**[⬆ voltar ao menu](#menu)**

## Objetos

### Sintaxe literal de objetos

* Use a sintaxe literal para criar objetos.

```js
// Bad
var foo = new Object();

// Good
var bar = {};
```

### Palavras reservadas

* Evite usar [palavras reservadas](http://es5.github.io/#x7.6.1) como chaves. Elas podem causar problemas em versões mais antigas do IE se não estiverem dentro de aspas.

```js
// Bad
var foo = {
  class: 'Foo'
};

// Good
var bar = {
  klass: 'Bar'
};

// Good
var baz = {
  type: 'Baz'
};
```

### Chaves de objeto

* Use :camel: camelCase ao nomear chaves de objetos, sempre quando possível.

```js
// Bad
var user = {
  'name': 'John',
  'has-children': false,
  'is-underage': false,
  'age': 42
};

// Good
var user = {
  name: 'John',
  hasChildren: false,
  isUnderage: false,
  age: 42
};
```

* Se você precisar usar aspas para envolver suas chaves, por qualquer motivo, use-o de maneira consistente:

```js
// Bad
var config = {
  development: true,
  'markdown-plugin': true,
  shouldIgnoreManifest: false,
  PersistData: true,
  enforcenamespace: true
};

// Good
var config = {
  'development': true,
  'markdown-plugin': true,
  'should-ignore-manifest': false,
  'persist-data': true,
  'enforce-namespace': true
};

// Good
var config = {
  development: true,
  markdownPlugin: true,
  shouldIgnoreManifest: false,
  persistData: true,
  enforceNamespace: true
};
```

**[⬆ voltar ao menu](#menu)**

## Arrays

### Sintaxe literal de arrays

* Use sintaxe literal para criação de arrays.

```js
// Bad
var foo = new Array();

// Good
var bar = [1, 2, 3];
```

### Adicionando itens

* Se você não sabe a quantidade de itens do array use `Array.push`.

```js
var groceries = [];

// Bad
groceries[groceries.length] = 'tomato';

// Good
groceries.push('oreo');
```

### Limpando array

* Para limpar um array, defina a quantidade como zero.

```js
// Bad
var foo = [1, 3, 5];
foo = null;

// Good
var bar = [2, 4, 6];
bar.length = 0;
```

### Conversão de array

* Para converter um objeto de matriz semelhante a uma matriz, use `Array.slice`.
* Você pode querer fazer isso porque objetos array-like (por exemplo, `{'0': 'Olá', '1': 'lá'}`) não têm métodos como `.join()`,
  para mais informações nesse assunto leia [esse artigo](http://nfriedly.com/techblog/2009/06/advanced-javascript-objects-arrays-and-array-like-objects/)

```js
function argsToArray() {
  var args = Array.prototype.slice.call(arguments);
}
```

**[⬆ voltar ao menu](#menu)**

## Strings

### Aspas

* Use aspas simples `''` para strings.

```js
// Bad
var morada = "Márcio Moradei";

// Good
var danilo = 'Danilo Vaz';
```

### Concatenação

* Concatene strings utilizando o operador mais `+`.

```js
var name = 'Danilo';

// Bad
name.concat('Vaz');

// Good
name += ' Vaz';
```

### Long strings

* Prefira concatenação de long strings, sempre adicionando quebras de linha depois de um operador. Long strings podem afetar o desempenho ([referências](http://jsperf.com/ya-string-concat) e [discussão](https://github.com/airbnb/javascript/issues/40)).

```js
// Bad
var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

// Bad
var errorMessage = 'This is a super long error that was thrown because \
of Batman. When you stop to think about how Batman had anything to do \
with this, you would get nowhere \
fast.';

// Good
var errorMessage = 'This is a super long error that was thrown because ' +
  'of Batman. When you stop to think about how Batman had anything to do ' +
  'with this, you would get nowhere fast.';
```

### Conversão de strings

* Para converter objetos em strings, use o método `toString()`.

* A conversão com `toString()` não funciona com valores `null` e `undefined`.
Para converter qualquer valor para string, concatene esse valor com uma string vazia. Isso é útil quando você não se importa com o valor da conversão (ex: em um logging ou tracking system).
No caso de você converter um valor `null`, ele será transformado em um `"null"`. A mesma regra é aplicada para valores `undefined`.

```js
var value = 42;

// Good
value += '';

var empty;

empty += ''; // "undefined"
```

**[⬆ voltar ao menu](#menu)**

## Funções

### Argumentos de funções

* Sempre que você tem mais de 3 argumentos sendo passados para uma função, é preferível você usar um objeto em seu lugar.

```js
// Bad

// Muitos argumentos
function setUser(firstName, lastName, age, gender, occupation) {
  // faz alguma coisa
}

setUser('Jon', 'Snow', 25, 'Male', 'Nights-watcher');

// Good

// Ao invés disso, use uma config/opções de objetos
function setUser(user) {
  // faz alguma coisa
}

setUser({
  firstName: 'Jon',
  lastName: 'Snow',
  age: 25,
  gender: 'Male',
  occupation: 'Nights-watcher'
});
```

## Convenções de nomenclatura

* Use camelCase quando nomear objetos, funções e instancias.

```js
// bad
var foo_bar = 'I am messed up';

// good
var fooBar = 'I am alright!';
```

* Use PascalCase quando nomear construtores e "classes".

```js
// Bad
function crewMember(name, role) {
  this.name = name;
  this.role = role;
}

var danilo = new crewMember('Danilo', 'Desenvolvedor');

// Good
function CrewMember(name, role) {
  this.name = name;
  this.role = role;
}

var alan = new CrewMember('Alan', 'Designer');
```

### Nomenclatura de funções

* Evite nomes com uma única letra. Seja descritivo e claro.

```js
// Bad
function f() {
  // What the hell is this?
}

// Good
function bootstrapFoo() {
  // Ah, ok!
}

// Bad
function stuff() {
  // "stuff" is too generic
}

// Good
function doAnimationStuff() {
  // Now we're talking
}
```

### Nomenclatura de construtores

* Sempre envolva as invocações de construtores entre brackets. Será mais fácil de passar novos valores no futuro.

```js
// Bad
var foo = new FooBar;

// Good
var bar = new FooBar();
var baz = new FooBar(1, 'lorem');
```

### Nomenclatura de propriedades privadas

* Utilize sempre um sublinhado inicial `_` ao nomear propriedades privadas e métodos.

```js
// Bad
var $name = 'Foo';
var __name = 'Bar';

// Good
var _name = 'Baz';
```

### Referenciando `this`

* Quando fizer um referência ao `this` nomei-o com `self`.

```js
// Bad
function() {
  var that = this;

  return function() {
    console.log(that);
  }
}

// Bad
function() {
  var _this = this;

  return function() {
    console.log(this);
  }
}

// Good
function() {
  var self = this;

  return function() {
    console.log(self);
  }
}
```

### Nomenclatura de booleanos

* Quando nomear variáveis booleanas, deve começar com "is", "has", "should" ou "was".

```js
// Bad
var ready = true,
    animate = true,
    started = false,
    animation = true;

// Good
var isReady = true,
    shouldAnimate = true,
    wasStarted = true,
    hasAnimation = true;
```

* Quando nomear funções booleanas, deve começar com "is".

```js
// Bad
function ready() {
  return false;
}

// Good
function isReady() {
  return true;
}
```

### Nomenclatura de acessores

* Quando nomear um acessor, tente começar com "get" or "set". Também nomeie explicitamente `value` como parâmetro getters.

```js
var currentStatus;

// Bad
function status(val) {
  if (val) {
    currentStatus = val;
  }

  return currentStatus;
}

// Good
function setStatus(value) {
  currentStatus = value;
}

function getStatus() {
  return currentStatus;
}
```

### Nomenclatura de event handlers

* Quando nomear um event handler (manipulador de evento), combine sua ação com o tipo de evento.

```js
// Bad
$('.button').click(click);

function click() {
  console.log('meh');
}

// Good
$('.button').click(toggleColorOnClick);

function toggleColorOnClick() {
  console.log('should toggle color on click!');
}
```

### Nomenclatura de seletores de elemento

* Ao nomear seletores de elementos nas classes DOM que terá qualquer tipo de comportamento, adicione o prefixo `js` para o nome do seu componente separando palavras usando um hífen `-`.

```html
<ul class="js-navigation-menu">
  <li>Foo</li>
  <li>Bar</li>
</ul>
```

```js
var menu = $('.js-navigation-menu');
```

**[⬆ voltar ao menu](#menu)**

## Propriedades

* Use o `.` para acessar as propriedades.

```js
var user = {
  name: 'John',
  age: 42
};

// Bad
var userName = user['name'];

// Good
var userAge = user.age;
```

* Use colchetes `[]` para acessar propriedades dinâmicas.

```js
var user = {
  name: 'John',
  age: 42
};

function getUserInfo(info) {
  return user[info];
}

var userName = getUserInfo('name');
```

**[⬆ voltar ao menu](#menu)**

## Expressões condicionais e de igualdade

* Use `===` e `!==` ao invés de `==` e `!=`.

**[⬆ voltar ao menu](#menu)**

## Blocos

* Sempre envolva blocos dentro de chaves e use novas linhas.

```js
// Bad
if (false)
  return;

// Bad
if (false) { return false; }

// Good
if (true) {
  return true;
}

// Good
if (true) {
  return true;
} else {
  return false;
}
```

**[⬆ voltar ao menu](#menu)**

## Comentários

* Não faça comentários insignificantes e óbvios, seja conciso sobre ele.

* Sinta-se livre para utilizar sintaxe markdown nos comentários.

* Não há necessidade de usar a sintaxe JSDoc uma vez que não geramos a documentação automaticamente.

* Usando tags `FIXME`, `TODO` e `NOTE` poderá ajudar outros desenvolvedores a entender e manter seu código. Você pode usar isso como quiser.

* Utilize sintaxe de bloco de documentação seguido por uma nova linha de comentários de várias linhas. Existem [ferramentas](#ferramentas) disponíveis para tornar isso realmente fácil.

```js
// Bad

// Usado para casar um `RegExp` de caracteres especiais.
// Veja esse [artigo sobre caracteres `RegExp`](http://www.regular-expressions.info/characters.html#special)
// para mais detalhes.

var matchSpecialChars = /[.*+?^${}()|[\]\/\\]/g;

// Bad

/*
Usado para casar um `RegExp` de caracteres especiais.
Veja esse [artigo sobre caracteres `RegExp`](http://www.regular-expressions.info/characters.html#special)
para mais detalhes.
*/

var matchSpecialChars = /[.*+?^${}()|[\]\/\\]/g;

// Good

/**
* Usado para casar um `RegExp` de caracteres especiais.
* Veja esse [artigo sobre caracteres `RegExp`](http://www.regular-expressions.info/characters.html#special)
* para mais detalhes.
*/

var matchSpecialChars = /[.*+?^${}()|[\]\/\\]/g;

```

* Use `//` para comentários de linha única. Coloque comentários de linha única sobre uma nova linha acima do assunto do comentário e adicione uma linha em branco antes do comentário.

```js
// Bad
var active = true;  // is current tab

// Good
// is current tab
var active = true;

// Bad
function getType() {
  console.log('fetching type...');
  // set the default type to 'no type'
  var type = this._type || 'no type';

  return type;
}

// Good
function getType() {
  console.log('fetching type...');

  // set the default type to 'no type'
  var type = this._type || 'no type';

  return type;
}
```

**[⬆ voltar ao menu](#menu)**

## Espaços em branco

### Tabs

* Use soft tabs definido para 2 espaços e nunca misture espaços com tabs.

```js
// Bad
function() {
∙∙∙∙var name;
}

// Bad
function() {
∙var name;
}

// Bad
function() {
⇥var name;
}

// Good
function() {
∙∙var name;
}
```

### EOF

* Sempre adicione uma linha em branco ao final do seu documento.

```js
// Bad
(function() {
  document.write('Hello World!');
})();

// Good
(function() {
  document.write('Hello World!');
})();
↵
```

### Declaração de condições e loop

* Coloque 1 espaço antes e depois de uma declaração de condição ou loop.

```js
// Bad
if(false){return false;}

// Good
if (true) {
  return true;
}

// Bad
while(false){console.log('whatever');}

// Good
while (false) {
  console.log('alright!');
}
```

### Operadores

* Separe os operadores com espaços.

```js
// Bad
var x=y+5;

// Good
var x = y + 5;
```

### Etapas de loop

* Coloque 1 espaço depois das etapas do loop e argumentos de função.

```js
// Bad
for(var i=0;i<10;++i) {
  console.log(i);
}

// Good
for (var i = 0; i < 42; ++i) {
  console.log(i);
}

// Bad
function setUser(name,surname,age){
  // sets user
}

// Good
function setUser(name, surname, age) {
  // sets user
}
```

### Declaração de objetos

* Em objetos que têm mais do que uma única propriedade você deve quebrar todas as propriedades em novas linhas.

```js
// Bad
var user = {name: 'John', surname: 'Doe', age: 42};

// Good
var user = {
  name: 'John',
  surname: 'Doe',
  age: 42
};
```

* Adicionar espaços internos quando declarar objetos embutidos.

```js
// Bad
var app = {locale: 'pt-br'};

// Good
var app = { locale: 'pt-br' };
```

### Encadeamento

* Use identação quando fizer longos encadeamentos de método.

```js
// Bad
$('#items').find('.selected').highlight().end().find('.open').updateCount();

// Good
$('#items')
  .find('.selected')
    .highlight()
    .end()
  .find('.open')
    .updateCount();
```

**[⬆ voltar ao menu](#menu)**

## Verificação de tipo

### String

```js
typeof variable === 'string';
```

### Número

```js
typeof variable === 'number';
```

### Booleano

```js
typeof variable === 'boolean';
```

### Objeto

```js
typeof variable === 'object';
```

### Array

```js
Array.isArray(arrayLikeObject);
```

### Node

```js
elem.nodeType === 1;
```

### `null`

```js
variable === null;
```

### `null` ou `undefined`

```js
variable == null;
```

### `undefined`

#### Variável global

```js
typeof variable === 'undefined';
```

#### Variável local

```js
variable === undefined;
```

### Propriedade

```js
object.prop === undefined;
object.hasOwnProperty(prop);
'prop' in object;
```

**[⬆ voltar ao menu](#menu)**

## Melhores práticas

* Não comece fechamentos com ponto e vírgula.

* Nós encorajamos você a registrar eventos da aplicação e mudanças importantes apenas no modo de desenvolvimento. Siga o formato de `Module/ClassName :: method() :: message`.

```js
function App() {
  console.log('App :: App instance created');
}

App.prototype.bootstrap = function() {
  console.log('App :: bootstrap() :: App was initialized');
};
```

### jQuery

* Cacheie consultas de jQuery sempre que possível.
* Prefira `remove()` ao invés de `empty()`.

**[⬆ voltar ao menu](#menu)**

## Links

### Artigos e posts

* [It’s time to start using JavaScript strict mode](http://www.nczonline.net/blog/2012/03/13/its-time-to-start-using-javascript-strict-mode)
* [Why is it recommended to have empty line in the end of file?](http://stackoverflow.com/questions/2287967/why-is-it-recommended-to-have-empty-line-in-the-end-of-file)
* [Multiple var statements in JavaScript, not superfluous](http://benalman.com/news/2012/05/multiple-var-statements-javascript)
* [Naming methods, properties and objects](http://blog.millermedeiros.com/naming-methods-properties-and-objects)

### Ferramentas

* [DocBlockr](https://sublime.wbond.net/packages/DocBlockr)
* [tcomment_vim](https://github.com/tomtom/tcomment_vim)
* [JSHint](http://www.jshint.com)
* [JSHint Plugins](http://www.jshint.com/install)
* [SublimeLinter](http://www.sublimelinter.com)
* [SublimeLinter-jshint](https://github.com/SublimeLinter/SublimeLinter-jshint)
* [How To Use SublimeLinter 3 (video)](http://youtu.be/u6fvJRao-E4)

**[⬅ voltar à página inicial](../../)**&nbsp;&nbsp;&nbsp;&nbsp;**[⬆ voltar ao menu](#menu)**
