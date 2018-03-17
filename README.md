# localized-strings
Simple module to localize the strings of any JS based program using the same syntax used in the 
[ReactLocalization module](https://github.com/stefalda/react-localization/) and
[ReactNativeLocalization module](https://github.com/stefalda/ReactNativeLocalization/) libraries.

## How it works

The library uses the current interface language, then it loads and displays the strings matching the current interface locale or the default language (the first one if a match is not found) if a specific localization can't be found.

It's possible to force a language different from the interface one.

It's possible to configure the library to use a specific routine that return the interface language, so it's possible to extend it in any possible environment.

## Installation
`npm install --save localized-strings`

## Usage

In the class that you want to localize require the library and define the strings object passing to the constructor a simple object containing a language key (i.e. en, it, fr..) and then a list of key-value pairs with the needed localized strings.

 ```js
\\ES6 module syntax
import LocalizedStrings from 'localized-strings';

let strings = new LocalizedStrings({
  en:{
    how:"How do you want your egg today?",
    boiledEgg:"Boiled egg",
    softBoiledEgg:"Soft-boiled egg",
    choice:"How to choose the egg"
  },
  it: {
    how:"Come vuoi il tuo uovo oggi?",
    boiledEgg:"Uovo sodo",
    softBoiledEgg:"Uovo alla coque",
    choice:"Come scegliere l'uovo"
  }
});
```

Then use the `strings` object literal directly in the render method accessing the key of the localized string.

```js
console.log ("HOW: " + strings.how);
```

## Custom getInterfaceLanguage method

You can pass a custom method to get the current interface based on the context.

The default method check the browser language but it could be replaced with other check if you are in a Server, ReactNative or Nativescript project.

The getInterfaceLanguage method can be as simple as:

```js
 function getCustomInterfaceLanguage(){
   return "it-IT";
 }
 
 let strings = new LocalizedStrings({
  en:{
    how:"How do you want your egg today?",
    boiledEgg:"Boiled egg",
    softBoiledEgg:"Soft-boiled egg",
    choice:"How to choose the egg"
  },
  it: {
    how:"Come vuoi il tuo uovo oggi?",
    boiledEgg:"Uovo sodo",
    softBoiledEgg:"Uovo alla coque",
    choice:"Come scegliere l'uovo"
  }
}, getCustomInterfaceLanguage)
```

## API

* setLanguage(languageCode) - to force manually a particular language
* getLanguage() - to get the current displayed language
* getInterfaceLanguage() - to get the current device interface language
* formatString() - to format the passed string replacing its placeholders with the other arguments strings
```js
  en:{
    bread:"bread",
    butter:"butter",
    question:"I'd like {0} and {1}, or just {0}"
    ...
    login: 'login',
    onlyForMembers: 'You have to {0} in order to use our app',
    bold: 'bold',
    iAmText: 'I am {0} text',
    ...
    january: 'January',
    currentDate: 'The current date is {month} {day}, {year}!'
  }
  ...
  strings.formatString(strings.question, strings.bread, strings.butter)

  // Named tokens can also be used to give some extra context to the format strings
  // You cannot mix tokens, something like formatString('{0}, {name}', 'Hello', {name: 'Bob'}) won't work
  strings.formatString(strings.currentDate, {
    month: strings.january,
    day: 12,
    year: 2018
  })
```
**Beware: do not define a string key as formatString!**

* setContent(props) - to dynamically load another set of strings
* getAvailableLanguages() - to get an array of the languages passed in the constructor

## Examples
To force a particular language use something like this:

```js
_onSetLanguageToItalian() {
  strings.setLanguage('it');
  this.setState({});
}
```

## Questions or suggestions?
Feel free to contact me on [Twitter](https://twitter.com/talpaz) or [open an issue](https://github.com/stefalda/localized-strings/issues/new).
