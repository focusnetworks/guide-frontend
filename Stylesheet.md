# `.focusnetworks {}`

Focusnetworks Stylesheet code styleguide.

## Menu

* [Disclaimer](#disclaimer)
* [Cores](#cores)
* [Unidades](#Unidades)
  * [Valores Nulo](#valores-nulo)
  * [Valores Float](#valores-float)
  * [`letter-spacing`](#letter-spacing)
  * [`line-height`](#line-height)
* [Imagens inline](#imagens-inline)
* [`!important`](#important)
* [Pseudo elementos](#pseudo-elementos)
* [Comentários](#Comentários)
* [Aspas](#aspas)
  * [Valores de Atributos](#valores-de-atributos)
  * [Background URL](#background-url)
* [Especificidade e aninhamento](#especificidade-e-aninhamento)
* [Convenções de nomenclatura](#convenções-de-nomenclatura)
  * [Classes de nomenclatura](#classes-de-nomenclatura)
  * [Nomenclatura de modificadores](#nomenclatura-de-modificadores)
  * [Nomenclatura de estados](#nomenclatura-de-estados)
* [Espaços em branco](#espaços-em-branco)
  * [Tabs](#tabs)
  * [EOF](#eof)
  * [Blocos inline](#blocos-inline)
  * [Nomes e valores de propriedades](#nomes-e-valores-de-propriedades)
  * [Declaração de blocos](#declaração-de-blocos)
  * [Multiplos seletores](#multiplos-seletores)
  * [Multiplas rules](#multiplas-regras)
  * [Multiplos valores](#multiplos-valores)
* [Links](#links)
  * [Artigos e posts](#artigos-e-posts)
  * [Ferramentas](#ferramentas)

## Disclaimer

Esse guia foi inspirado por [Mark Otto's Code Guide](http://mdo.github.io/code-guide/#css) e [Idiomatic CSS](https://github.com/necolas/idiomatic-css).

## Cores

* Escrever valores de cores hexadecimais sempre em lowercase. Use notação abreviada quando possível.

```css
// Bad
color: #CCCCCC;

// Good
color: #ccc;

// Bad
color: red;

// Good
color: #ff0066;

// Bad
color: #EAEAE2;

// Good
color: #eaeae2;
```
**[⬆ voltar ao topo](#menu)**

## Unidades

### Valores Nulo

* Evite especificar unidades para valores nulo

```css
// Bad
.square {
  border: 0px;
}

// Good
.square {
  border: 0;
}
```

### Valores Float

* Não coloque zero à esquerda em valores float

```css
// Bad
.heading {
  margin-left: -0.75px;
}

// Good
.heading {
  margin-left: -.75px;
}
```

### `letter-spacing`

* Use unidades `pt` para declarar valores `letter-spacing`. Nós achamos que é mais fácil de combinar as especificações visuais do Photoshop.

```css
// Bad
.text {
  letter-spacing: -.75px;
}

// Good
.text {
  letter-spacing: -.75pt;
}
```

### `line-height`

* Não adicione unidades para valores `line-height`.

```css
// Bad
p {
  line-height: 1.55px;
}

// Good
p {
  // Equivalente a 150% do tamanho da fonte
  line-height: 1.5;
}
```

**[⬆ voltar ao topo](#menu)**

## Imagens inline

* Imagens inline só são permitidas se o seu tamanho for menor que **1KB** e presentes apenas uma vez no code. Evite imagens inline.

**[⬆ voltar ao topo](#menu)**

## `!important`

* Se você não pode explicar o por que de um `!important` ser importante, provavelmente não é importante :sunglasses:

**[⬆ voltar ao topo](#menu)**

## Pseudo elementos

* Pseudo elementos devem ser acessados usando uma vez dois pontos `:`. Não use duas vezes o dois pontos `::`.

```css
// Bad
.button::before {
  outline: 1px solid;
}

// Good
.button:after {
  background: fuchsia;
}
```

**[⬆ voltar ao topo](#menu)**

## Comentários

* A estrutura de comentário deverá seguir o seguinte padrão:

```css
/* ==========================================================================
   Nome do component
   ========================================================================== */

/**
 * Alguma descrição sobre o meu component
 * Sempre tente ser conciso e direto!
 */

.component {
  // ...
}

```

**[⬆ voltar ao topo](#menu)**

## Aspas

* Sempre use aspas duplas `"`.

```css
// Bad
.selector:after {
  content: 'Foo Bar';
}

// Good
.selector:before {
  content: "Lorem Ipsum";
}
```

### Valores de atributos

* Use aspas nos valores de atributos.

```css
// Bad
input[type=radio] {
  display: none;
}

// Good
input[type="number"] {
  opacity: 1;
}
```

### Background URL

* Use aspas nas urls de backgrounds.

```css
// Bad
.selector {
  background: url(path/to/image.png) no-repeat;
}

// Good
.selector {
  background: url("path/to/image.png") no-repeat;
}
```

**[⬆ voltar ao topo](#menu)**

## Especificidade e aninhamento

* Evite escrever seletores excessivamente específicos e um grande número de normas aninhadas. Separe-os quando a legibilidade começar a ser afetada.
* Máximo de **3** níveis de aninhamento.

```css
// Bad
.menu {
  background: orange;
  .menu-item {
    font-family: sans-serif;
    .link {
      &:hover {
       color: red;
      }
      > .link-label {
        font-weight: bold;
      }
    }
  }
}

// Good
.menu {
  background: orange;
}

.menu-item {
  font-family: sans-serif;
}

.link:hover {
  color: red;
}

.link-label {
  font-weight: bold;
}
```

**[⬆ voltar ao topo](#menu)**

## Convenções de nomenclatura

### Classes de nomenclatura

* Classes devem ser nomeadas separando espaços menores com um hífen `-`.

```css
// Bad
.fooBar {
  border: none;
}

// Good
.foo-bar {
  outline: 1px solid red;
}

// Bad
.LoremIpsumDolor {
  text-align: center;
}

// Good
.lorem-ipsum-dolor {
  vertical-align: middle;
}
```

### Nomenclatura de modificadores

* Modificadores devem ter o módulo de base como um prefixo e o nome do modificador separados por hífens duplos `--`.

```css
.logo {
  background: url("./logo.png") no-repeat;
}

// Bad
.logoBig {
  transform: scale(1.5);
}

// Good
.logo--big {
  transform: scale(1.25);
}

// Bad
.logo-with-small-size {
  transform: scale(.25);
}

// Good
.logo--small {
  transform: scale(.5);
}
```

### Nomenclatura de estados

* Estados devem indicar um estado, como o nome sugere. Sempre comece estados com "is", "has", "should" ou "was"

```css
// Bad
.logo.logoHidden {
  opacity: 0;
}

// Good
.logo.is-hidden {
  opacity: 0;
}

// Bad
.logo.logo-with-border {
  border: 1px solid;
}

// Good
.logo.has-border {
  border: 1px solid fuchsia;
}
```

**[⬆ voltar ao topo](#menu)**

## Espaços em branco

### Tabs

* Use soft tabs definido para 2 espaços e nunca misture espaços com tabs.

```css
// Bad
.foo {
∙∙∙∙border: 1px solid red;
}

// Bad
.bar {
∙display: block;
}

// Bad
.baz {
⇥width: 100%;
}

// Good
.lorem {
∙∙box-sizing(border-box);
}
```

### EOF

* Sempre adicione uma linha em branco ao final do seu documento.

```css
// Bad
.main {
  background: red;
}

// Good
.main {
  background: blue;
}
↵
```

### Blocos inline

* Somente seletores com uma única propriedade estão autorizados a ser declarada inline, adicione quebras de linha, se houver mais do que um único.

```css
// Bad
.section { cursor: pointer; text-align: center; }

// Good
.section { cursor: default; }

// Good
.section {
  text-align: left;
  vertical-align: middle;
}
```

### Nomes e valores de propriedades

* Sempre adicionar um espaço em branco entre nomes de propriedades e valores.

```css
// Bad
.selector {
  top:0;
  left:0;
}

// Good
.selector {
  top: 10px;
  left: 15px;
}
```

### Declaração de blocos

* Inclua um espaço antes da chave de blocos de declaração de abertura.

```css
// Bad
.selector{
  vertical-align: baseline;
}

// Good
.selector {
  vertical-align: middle;
}
```

### Multiplos seletores

* Na segmentação de vários seletores quebrar cada um em uma nova linha.

```css
// Bad
.footer, .header, .main {
  display: block;
}

// Good
.footer,
.header,
.main {
  margin: 0 auto;
}
```

### Multiplas regras

* Mantenha várias regras em uma única linha, mas adicione um espaço em branco após cada vírgula.

```css
// Bad
.box {
  box-shadow: 0 1px 1px #eee,
  inset 0 1px 0 #f00;
}

// Good
.box {
  box-shadow: 0 1px 1px #eee, inset 0 1px 0 #f00;
}
```

### Multiplos valores

* Adicionar um espaço em branco após cada vírgula em vários valores.

```css
// Bad
.selector {
  background: rgba(0,0,0,.5);
}

// Good
.selector {
  background: rgba(255, 255, 255, .75);
}
```

**[⬆ voltar ao topo](#menu)**

## Links

### Artigos e posts

* [Improving Code Readability With CSS Styleguides](http://www.smashingmagazine.com/2008/05/02/improving-code-readability-with-css-styleguides/)
* [Line-Height Units](http://tzi.fr/css/text/line-height-units)

### Ferramentas

* [CSSLint](https://github.com/CSSLint)
* [SublimeLinter-csslint](https://github.com/SublimeLinter/SublimeLinter-csslint)
* [csslint.vim](http://www.vim.org/scripts/script.php?script_id=3823)
* [st-snippets](https://github.com/rafaelrinaldi/st-snippets/tree/master/comments)

**[⬅ voltar à página inicial](../../)**&nbsp;&nbsp;&nbsp;&nbsp;**[⬆ voltar ao topo](#menu)**
