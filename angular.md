---
layout: page
title: Angular
permalink: /angular/
---
**AngularJS** - otwarta biblioteka / [framework](http://pl.wikipedia.org/wiki/Framework) języka JavaScript, wspierana i firmowana przez Google, 
wspomagająca tworzenie i rozwój aplikacji internetowych na pojedynczej stronie (single page application). 
Zadaniem biblioteki jest wdrożenie wzorca [Model-View-Controller (MVC)](http://pl.wikipedia.org/wiki/MVC) 
do aplikacji internetowych, aby ułatwić ich rozwój i testowanie.  

To co wyróżnia AngularJS spośród innych tego typu frameworków to własny kompilator HTML. 
Pozwala nam on „nauczyć” naszego HTML nowych sztuczek, zachowań i dodać mu kilka funkcjonalności. 
W ten sposób jesteśmy w stanie zbudować dynamiczną aplikację internetową.

## Framework

W programowaniu komputerowym framework (ang. framework - struktura) albo platforma programistyczna jest szkieletem do budowy aplikacji. 
Definiuje on strukturę aplikacji oraz ogólny mechanizm jej działania, a także dostarcza zestaw komponentów 
i bibliotek ogólnego przeznaczenia do wykonywania określonych zadań.  

> Zamiast pisać kod tak jak Ty chcesz, dostoswowujesz się do założeń 
> i narzędzi danego framework'a.
> 
> Dzięki temu masz dostęp do wbudowanych udogodnien takich jak system 
> szablonów, filtry i wiele więcej.
{: .info}

## Single Page Application

Główną różnicą pomiędzy modelem Single Page Application (SPA), a standardowymi aplikacjami jest jednostronicowy interfejs 
oraz przeniesienie logiki z serwera na klienta. Cała logika aplikacji jest napisana po stronie klienta w JavaScript
 i wykonywana w przeglądarce. Kod HTML, JavaScript i CSS jest pobierany jednorazowo w trakcie uruchomienia aplikacji, 
 natomiast pozostałe wymagane zasoby zostaną pobrane dynamicznie, gdy będą potrzebne w danej chwili. 
 Przykładem jednej z wielu aplikacji SPA jest Gmail.

> AngularJS został zaprojektowany tak aby wspierać model 
> Single Page Application.
{: .info}

## Dlaczego warto używać AngularJS?

* Oszczędność czasu dzięki wbudowanym funkcjonalnościom
* Wbudowany system szablonów
* Świetna obsługa DOM (Two Way Binding, Dirty Checking)
* Łatwy i przyjemny sposób manipulowania danymi (Ajax, MVC)
* Forward thinking (pol. myślenie wprzód)
* Dependency injection

> AngularJS już dziś pozwala nam na używanie elementów HTML/JS, które 
> kiedyś będą standardem (Web Components, Object.observe).
{: .info}

## Model-View-Controller (MVC)

Model-View-Controller (pol. Model-Widok-Kontroler) jest to wzorzec projektowy zakładający podział aplikacji na Model, Widok i Kontroler gdzie:

* **M**odel - jest reprezentacją danych w aplikacji.
* **V**iew - opisuje, jak wyświetlić pewną część modelu w ramach interfejsu użytkownika. 
* **C**ontroller - przyjmuje dane wejściowe od użytkownika i reaguje na jego poczynania, zarządzając aktualizacją modelu oraz odświeżaniem widoków.

## Główne fukcjonalności

* **Directives** (pol. Dyrektywy) Dyrektywa, to właśnie sposób na nauczenie HTML nowych sztuczek.
AngularJS w fazie kompilacji ($compile) skanuje drzewo DOM naszego dokumentu HTML, 
a następnie w miejsce wystąpień dyrektyw podpina funkcjonalności na poziomie samego DOM. 
Owe funkcjonalności mają zastosowanie na poziomie elementu, dla którego zdefiniowaliśmy dyrektywę oraz wszystkich jego dzieci. 
Dyrektywy pozwalają w ten sposób budować reużywalne komponenty, które pozwalają manipulować 
drzewem DOM oraz dostarczać mu nowych funkcjonalności np: **ng-app** lub **ng-model**.

<prism-js language="markup" escape><!--
<!doctype html>
<html lang="en" ng-app>
<head>
  <meta charset="UTF-8">
  <title>Acodemy.io</title>
  <script src="angular.js"></script>
</head>
<body>
  <input type="text" ng-model="name">
  <h2>Cześć {% raw %}{{name}}{% endraw %}</h2>
</body>
</html>
--></prism-js>

* **Data binding** mechanizm pozwalający aplikacjom w prosty i spójny sposób prezentować i modyfikować dane. 
Pozwala oddzielić logikę aplikacji od interfejsu użytkownika.

![Data binding]({{ site.baseurl }}img/two_way_data_binding.png)

* **Filters** (pol. Filtry) umożliwiają modyfikację danych wejściowych, formatowanie oraz sortowanie. 
* **Modules** (pol. Moduły) pozwalają nam podzielić aplikację na mniejsze łatwiejsze w zarządzaniu fragmenty

<source-switcher>
<prism-js language="coffeescript">
app = angular.module 'acodemy', [
  'ngRoute'
  'acodemyControllers'
]
</prism-js>
<prism-js language="javascript">
var app = angular.module('acodemy', [
  'ngRoute'
  'acodemyControllers'
]);
</prism-js>
</source-switcher>

* **Routes** (pol. Ścieżki) kluczowy element SPA pozwala on nam "symulować" przechodzenie pomiędzy różnymi stronami oraz
usprawnia podział aplikacji na logiczne fragmenty.

<source-switcher>
<prism-js language="coffeescript">
app = angular.module 'acodemy', [
  'ngRoute'
  'acodemyControllers'
]

app.config ($routeProvider) ->
  $routeProvider.
    .when '/list',
      templateUrl: 'views/list.html'
      controller: 'ListController'
    .when '/details/:id', 
      templateUrl: 'views/details.html'
      controller: 'DetailsController'
    .otherwise
      redirectTo: '/list'
</prism-js>
<prism-js language="javascript">
var app = angular.module('acodemy', [
  'ngRoute'
  'acodemyControllers'
]);

app.config(function($routeProvider) {
  $routeProvider.
    .when('/list', {
      templateUrl: 'views/list.html',
      controller: 'ListController'
    })
    .when('/details/:id', {
      templateUrl: 'views/details.html',
      controller: 'DetailsController'
    })
    .otherwise({
      redirectTo: '/list'
    });
});
</prism-js>
</source-switcher>

* **Controllers** (pol. Kontrolery) to spoiwo łączące nasze modele z widokami pozwalające na obsługe interakcji z użytkownikiem.

<source-switcher>
<prism-js language="coffeescript">
app.controller 'ListController', ($scope) ->
  $scope.sayHi = () ->
    alert 'Hi!'
</prism-js>
<prism-js language="javascript">
app.controller('ListController', function($scope) {
  $scope.sayHi = function() {
    alert('Hi!');
  };
});
</prism-js>
</source-switcher>
