---
layout: page
title: Webcom
permalink: /Webcom/
---
![Web Components]({{ site.baseurl }}/img/web-components-logo.svg)

Web Components jest to zbiorcza nazwa na zestaw 4 specyfikacji, które razem
pozwalają na tworzenie własnych typów elementów DOM.

## HTML Imports

Ponieważ tworzone komponenty mogą zawierać zarówno szablony, style jak i kod (logikę komponentu), aby ułatwić włączanie komponentów do aplikacji dodano możliwość załączenia dokumentu HTML wewnątrz drugiego, podobnie jak załączamy style czy skrypty.

<prism-js language="markup" escape><!--
<link rel="import" href="components/my-tag.html">
--></prism-js>

## Templates

Specyfikacja wprowadza nowy element `<template>`, którego zawartość nie jest wykorzystywana przez przeglądarkę dopóki aplikacja nie poprosi o stworzenie jej kopii. Eliminuje to problemy związane z przedwczesnym ładowaniem danych np. pobieraniem obrazów przez tag `<img>` zanim zostanie ustawione odpowiednie źródło (`src`).

<prism-js language="markup" escape><!--
<template id="soo-reusable-div">
  <div class="info">
    <p>Div which you will meet N times</p>
    <img src="image.png">
  </div>
</template>
<script>
  var template = document.querySelector('#soo-reusable-div');
  var clone = document.importNode(template.content, true);
  document.body.appendChild(clone);
</script>
--></prism-js>

> Przy pomocy drugiego argumentu funkcji importNode mówimy, czy chcemy wykonać deep import. Na tę chwilę default value jest różne w różnych przeglądarkach.
{: .info}


## Shadow DOM

Shadow DOM wprowadza enkapsulację do DOM'u. Każdy element może mieć shadow root, który jest wyświetlany zamiast faktycznej zawartości. Typowym przykładem jest tag `<video>`. Jego Shadow DOMem jest prostokąt, na którym rysowany jest film, z przyciskami odtwarzania/pauzy, paskiem do przewijania filmu itd. Style i kod potrzebny do wyświetlenia tego widgetu są odseparowane od dokumentu, w którym się znajduje.

Poniżej przykład ze strony youtube.com i wycinek webinspectora z głównego, odtwarzanego filmu:

![Shadow DOM Video tag]({{ site.baseurl }}web_components/img/shadow_dom-video.png "Shadow DOM Video tag")


## Custom Elements

Ostatnia specyfikacja wprowadza sposób definiowania własnych elementów/tag'ów oraz dostarcza metody kontrolowania ich cyklu życia, co pozwala na dodanie odpowiedniej logiki do elementu. Dzięki temu nasz kod może być bardziej samoopisujący i czytelniejszy.

Dobrym przykładem webcomponentu jest element, który na pewno każdy z Was widział, a nie koniecznie zdawał sobie z tego sprawę. 'Timeago' na githubie wykorzystuje prosty webcomponent, który co minutę przelicza ile czasu upłynęło od daty która znajduje się w jego wnętrzu oraz wyświeta ją w innej, bardziej przyjaznej formie. 

W poniższym przykładzie element time jest rozszerzany przy pomocy atrybutu `is` elementem time-ago. Widzimy jak data przekazana w atrybucie zostaje zamieniona na nowy format.


![Custom Element time ago]({{ site.baseurl }}web_components/img/web_components-timeago.png "Custom Element time ago")


## Web Component

Poniżej przykład użycia wszystkich czterech elementów w celu zbudowania kompletnego komponentu.

`say-hello.html`

<prism-js language="markup" escape><!--
<template id="sayHelloTemplate">
  <style>
    span { color: red; }
  </style>
  <p>Hello <span><content></content></span>!</p>
</template>
<script src="say-hello.js"></script>
--></prism-js>

`say-hello.js`

<source-switcher>
<prism-js language="coffeescript">
class SayHello extends HTMLElement
  createdCallback: ->
    shadow = @createShadowRoot()
    shadow.appendChild
      document.getElementById('sayHelloTemplate').content

document.registerElement 'say-hello', SayHello
</prism-js>
<prism-js language="javascript">
function SayHello() {}
SayHello.prototype = Object.create(HTMLElement.prototype);
SayHello.prototype.createdCallback = function() {
  var shadow = this.createShadowRoot();
  shadow.appendChild(
    document.getElementById('sayHelloTemplate').content
  );
};

document.registerElement('say-hello', SayHello); 
</prism-js>
</source-switcher>

`index.html`

<prism-js language="markup" escape><!--
<link rel="import" href="say-hello.html"> 
<say-hello>Web Components</say-hello>
--></prism-js>

> Hello <span style="color: red">Web Components</span>!

## Polymer

Jest to biblioteka stworzona przez Google'a która ma na celu łatwiejsze i szybsze tworzenie webcomponentów (syntax sugar). Dodatkowo, Polymer jest w stanie zapewnić polyfill funkcjonalności ShadowDOM w przeglądarkach, które go nie obsługują. Więcej informacji można znaleźć pod [tym adresem](https://www.polymer-project.org/).

<prism-js language="markup" escape><!--
<link rel="import" href="polymer.html">

<dom-module id="say-hello">
  
  <template>
    <style>
      span { color: red; }
    </style>

    <p>Hello <span><content></content></span>!</p>
  </template>

  <script>
    Polymer({is: 'say-hello'})
  </script>
</dom-module>
--></prism-js>
