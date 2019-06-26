![Sitecore Speedy](https://aceiksolutions.files.wordpress.com/2019/06/speedylogo.png?w=1024&h=321)

## Sitecore Speedy (SXA Version) 
<img src='https://img.shields.io/github/tag/Aceik/Sitecore-Speedy.svg' />
<img src='https://img.shields.io/github/issues/Aceik/Sitecore-Speedy.svg' />
<img src='https://img.shields.io/github/license/Aceik/Sitecore-Speedy.svg' />
<img src='https://img.shields.io/github/languages/code-size/Aceik/Sitecore-Speedy.svg' />

Use best practice page load techniques to achieve Outstanding Page Speed scores for your Sitecore pages. 

## What does it do ?

Speedy provides a Sitecore Layout and Asset provider that structures your HTML in accordance with Google's recommendations.  Google ranks your website with a score out of 100 and provides recommendation on how to achieve better scores.
Implementing Critical CSS and Deferred Javascript loading can be tricky. This module provides a framework and the tools needed to automate the process. 

## What structure is this module written in ?

This is a Sitecore Helix module. 

It is planned to release this module as an installable Sitecore package as well.

## What does Speedy solve in regard to Page Speed ?

In order to get great page speed scores there are several aspects you need to address. [Read more here.](https://github.com/Aceik/Sitecore-Speedy/wiki/Page-Speed-Considerations)

This module addresses Critical CSS and Deferred asset loading, which is perhaps one of the hardest parts of Page Speed to get right.

## Getting Started Steps
1) [installation](https://github.com/Aceik/Sitecore-Speedy/wiki/Installation)
2) [installation](https://github.com/Aceik/Sitecore-Speedy/wiki/Installation)

## Installation prerequisites

Pre-Requisuits 
1) <img src="https://img.shields.io/badge/requires-node-blue.svg?style=flat-square" alt="requires node">  (Required in [local development mode](https://github.com/Aceik/Sitecore-Speedy/wiki/Development-Mode))
2) <img src="https://img.shields.io/badge/requires-sitecore-blue.svg?style=flat-square" alt="requires node">

## Installation

Read about [installation via source code.](https://github.com/Aceik/Sitecore-Speedy/wiki/Installation)

## Critical Generation 

Read about [critical generation options](https://github.com/Aceik/Sitecore-Speedy/wiki/Critical-Generation-Options)

## Usage on a Page

Which ever page you now choose to use Speedy on, navigate to that item:
	
- Make a new version of the item, so that you can roll back if needed.
- Presentation > Details > Final Layout :  Change the layout to 
> Layouts/Foundation/Speedy/MVC/MVC Layout Page Speed
- Save and publish the item

## Time to Adapt  - Tweak and Test

After following the above instructions its time to run the Lighthouse Audit in your browser and check your page speed score. 

Different pages will have different features, javascript and appearance. The end result that you get using these techniques can be different on every page.

At the end of the day what your trying to achieve is something like this:

- Display the HTML and CSS of the viewport so that First Contentful Paint happens as soon as possible.  Hide DOM object that require javascript to be full loaded. 

- After a certain period start loading external resources. 

- After loading resources begin to show DOM object that require all the javascript to be loaded and parsed by the browser. These resources are original hidden using Vanilla JS and are now made visible. (Fallback Experience)

##### NOTE:  Javascript by far has the most impact on this whole process as it is the most expensive asset a users browser will download, parse (code parse) and ultimately run. 

This module has some options available for tweaking and retesting. 

| Name          						| Field Name           	| Description  |
| ------------- 						|:-------------:		| -----:|
| Defer JS Load For Milliseconds      	| The length of time to delay the load of external Javscript assets for (in milliseconds) 		| $1600 |
| Defer CSS Load For Milliseconds      	| The length of time to delay the load of external CSS assets for (in milliseconds)      		|   $12 |
| Defer Fallback Load For Milliseconds 	| The length of time to delay the visibility of certain DOM elements (in milliseconds). Based on the next setting. 				|		|
| CSS Fallback Experience Selector 		| This css selector is done on a per page basis and allows the hiding and showing of DOM elements in order to support a Fallback Experience.     				|		|

-----------------------

## Complex Issues

In reality there is nothing simple about getting Critical and Javascript to play together. 

This process will take some trial and error, the aim of which is to present the user with an experience that is so quick that they don't notice and strange behaviour at all.

Strange behaviour usually includes flashing or mutating elements (in the blink of eye) as the deferred page load assets are loaded into the DOM.  This is due to the fact that these assets are delayed and once they are loaded they each impact the DOM in turn.

[Read more about how to handle ...](https://github.com/Aceik/Sitecore-Speedy/wiki/Complex-Page-Speed-Issues)


### Sitecore Settings


#### Global

The following settings will be installed at the following location: /sitecore/system/Settings/Foundation/Speedy/Speedy Global Settings

| Setting Name        | Example Values           | Notes |
| ------------- |:------------------------:|:-----:|
| Endpoint URL         | https://nodeapicritical.azurewebsites.net/critical/ |  This URL points to your hosted version of the node JS web application that run the critical script. [Read more about production mode](https://github.com/Aceik/Sitecore-Speedy/wiki/Production-Mode) |
| ShouldRegenerateOnEverySaveEvent  | true/false      |  Attempt to generate critical on save of each page. Critical must be enabled on a page for this to kick in. |
| CookieExpirationDays | 10      |  When first pass only mode is enabled this controls how long the cookie is valid for.  [Read More](https://github.com/Aceik/Sitecore-Speedy/wiki/Page-Speed---First-Pass-Mode) |
| DeferJSLoadForMilliseconds  |   4000    |  This value is in milliseconds. [Read More](https://github.com/Aceik/Sitecore-Speedy/wiki/Deferred-Javascript) |
| DeferCSSLoadForMilliseconds |  5500    | Value in milliseconds.   We are using Critical CSS to make sure FCP happens nice and early without the need for external CSS assets.  This value controls how long we wait until the external assets are asked to kick into gear.  | 
| DeferFallbackForMilliseconds  |   5000   |  Value in milliseconds.  [Read about first pass mode](https://github.com/Aceik/Sitecore-Speedy/wiki/Page-Speed---First-Pass-Mode)  |


## References and Inspiration

* [Deep dive into the murky waters of script loading](https://www.html5rocks.com/en/tutorials/speed/script-loading/)
* [Async Vs Defer](https://bitsofco.de/async-vs-defer/)
* [Efficiently load JavaScript with defer and async](https://flaviocopes.com/javascript-async-defer/)
* [Critical](https://www.npmjs.com/package/critical)
* [LoadCSS](https://github.com/filamentgroup/loadCSS/blob/master/README.md) -- Looking to implement this in a future version
* https://www.browserless.io/
