---
layout: post
title: Instalacja
order: 3
---

## Szablon aplikacji

Abyś w pełni mógł cieszyć się kodowaniem w `AngularJS`, i nie zaprzątał sobie głowy takimi drobnostkami jak HTML czy CSS,
przygotowaliśmy dla Ciebie [szablon](https://github.com/10clouds/acodemy-spotify/archive/template.zip).

> #### Zadanie dla Ciebie:
> 
> * Pobierz [szablon](https://github.com/10clouds/acodemy-spotify/archive/template.zip)
> * Rozpakuj i uruchom w przeglądarce `src/index.html`
> * Wystartuj serwer http w katalogu `src` wykorzystując np. 
>   pythonowy [SimpleHTTPServer](https://docs.python.org/2/library/simplehttpserver.html)
> * Pytania?
{: .warning}

### Efekt

![Szablon]({{site.baseurl}}/intro/img/template.png)

<prism-js language="bash">
acodemy-spotify
├── .bowerrc
├── .gitignore
├── bower.json
├── gulpfile.js
├── package.json
└── src
    ├── album
    │   └── index.html
    ├── artist
    │   └── index.html
    ├── bower
    │   ├── angular
    │   ├── angular-route
    │   ├── core-component-page
    │   ├── font-awesome
    │   ├── normalize.css
    │   ├── polymer
    │   └── webcomponentsjs
    ├── index.html
    └── styles.css
</prism-js>


## Narzędzia

> #### Zalecane
> 
> Polecamy skorzystać z poniższych narzędzi, usprawnią one nasze dalsze prace. 
> 
> Jednak jeśli zainstalowanie któregoś z nich okaże się 
> problematyczne, np. ze względu na system operacyjny, cały kurs można 
> przejść korzystając tylko z podstawowego serwera HTTP, np. pythonowego 
> [SimpleHTTPServer](https://docs.python.org/2/library/simplehttpserver.html).
{: .warning}

Aby rozpocząc naszą przygodę z AngularJS na profesjonalnym poziomie będziemy potrzebowali zainstalować:

* NodeJS - [nodejs.org](http://nodejs.org/)
* NPM - [npmjs.com](https://npmjs.com/)
* CoffeeScript - [coffeescript.org](http://coffeescript.org/)
* Gulp - [gulpjs.com](http://gulpjs.com/)
* Bower - [bower.io](http://bower.io/)


### NodeJS & NPM

`Node.js` jest środowiskiem programistycznym zaprojektowanym do tworzenia wysoce skalowalnych aplikacji internetowych, szczególnie serwerów www napisanych w języku JavaScript. 
`Node.js` umożliwia tworzenie aplikacji sterowanych zdarzeniami wykorzystujących asynchroniczny system wejścia-wyjścia.


Dla ubuntu Ubuntu 13.10 i 14.04 sytuacja jest bardzo prosta:

<prism-js language="bash">
sudo apt-get install nodejs npm
</prism-js>

Jeżeli posiadacie starszą wersje Ubuntu sytuacja nieco się komplikuje:

<prism-js language="bash">
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:chris-lea/node.js
sudo apt-get update
sudo apt-get install nodejs
</prism-js>


Dla OSX:

Jeżeli posiadacie zainstalowany 
<prism-js language="bash">
http://nodejs.org/dist/v0.10.36/node-v0.10.36.pkg
</prism-js>

Dodatkowo, całkiem niezły spis how-to można znaleźć na [githubie node'a](https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager)

> #### Ubuntu
> 
> W starszych wersjach Ubuntu pakiety `NodeJS` są przedawnione. 
> Ich instalacja może spodowdować brak kompatybilności z pozostałymi 
> aplikacjami.
{: .danger}

Jeżeli masz szczęście i nie używasz Ubuntu to w pozostałych dystrybucjach sytuacja wygląda znacznie prościej:

<prism-js language="bash">
# Fedora
sudo yum install nodejs npm

# Arch Linux
sudo pacman -S nodejs

# openSUSE & SLE
sudo zypper ar http://download.opensuse.org/repositories/devel:/languages:/nodejs/openSUSE_13.1/ Node.js
sudo zypper in nodejs nodejs-devel

# Gentoo
emerge nodejs
</prism-js>

### Bower

`Bower` jest managerem pakietów dla aplikacji web'owych. Pomaga zarządzać zależnościami po stronie frontendu aplikacji. Wykorzystamy go później, żeby zainstalować potrzebne nam bootstrap, angular, polymer oraz ich wszystkie zależności.

<prism-js language="bash">
# Instalacja globalna - zalecana
sudo npm install -g bower

# Instalacja lokalna
npm install bower
</prism-js>

### CoffeeScript

`CoffeeScript` to język programowania kompilowany do JavaScriptu. 
`CoffeeScript` dodaje lukier składniowy zainspirowany przez Ruby'ego i Pythona aby zwiększyć czytelność kodu. 
Język oferuje także bardziej wyrafinowane funkcje, takie jak przetwarzanie tablic i dopasowywanie do wzorców. 
Ponieważ `CoffeeScript` kompiluje się do JavaScriptu, programy mogą być krótsze o około 1/3 bez strat dla szybkości działania. 


<prism-js language="bash">
# Instalacja globalna - zalecana
sudo npm install -g coffee-script

# Instalacja lokalna
npm install coffee-script
</prism-js>

> #### JavaScript
> 
> Jeśli nie jesteś fanem CoffeeScript i wolałbyś przejść cały kurs posługując
> się samym JavaScript'em, wszystkie fragmenty kodu w instrukcjach są dostępne 
> zarówno w Coffee jak i JavaScripcie.
> 
> <source-switcher>
> <prism-js language="coffeescript">
> $http.get('/resource')
> .then (response) ->
>   $scope.data = response.data
> .catch (response) ->
>   console.error "couldn't fetch resource: #{response.status}"
> </prism-js>
> <prism-js language="javascript">
> $http.get('/resource')
> .then(function(response) {
>   $scope.data = response.data;
> })
> ["catch"](function(response) {
>   console.error("couldn't fetch resource: " + response.status);
> });
> </prism-js>
> </source-switcher>
{: .warning}

### Gulp

`Gulp` ułatwi Ci życie, zautomatyzuje za Ciebie cały proces budowania, konkatenacji (łączenia tekstu, w tym przypadku - kodu), wersjonowania oraz kompresji naszej aplikacji.

<prism-js language="bash">
# Instalacja globalna - zalecana
sudo npm install -g gulp

# Instalacja lokalna
npm install gulp
</prism-js>

### Weryfikacja <small>nareszcie to już koniec :P</small>

<prism-js language="bash">
$ node -v
v0.10.36

$ npm -v
1.4.28

$ bower -v
1.3.12

$ coffee -v
CoffeeScript version 1.7.1

$ gulp -v
CLI version 3.8.10
</prism-js>

> #### Zadanie dla Ciebie:
> 
> * Zainstaluj: NodeJS, CoffeeScript, Gulp oraz Bower
> * Zweryfikuj poprawność instalacji
> * Zapoznaj się z możliwościami poszczególnych pakietów
> * Zainstaluj zależności naszej aplikacji wykorzystując `npm` i `bower`
> * Wystartuj serwer http za pomocą `gulp`
> * Jeżeli nigdy nie programowałeś w `CoffeeScript` to jest dobry 
>   moment na zapoznanie się ze składnią
> * Pytania?
{: .warning}

