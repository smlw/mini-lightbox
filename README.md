
# mini-lightbox

 [![Support me on Patreon][badge_patreon]][patreon] [![Buy me a book][badge_amazon]][amazon] [![PayPal][badge_paypal_donate]][paypal-donations] [![Version](https://img.shields.io/npm/v/mini-lightbox.svg)](https://www.npmjs.com/package/mini-lightbox) [![Downloads](https://img.shields.io/npm/dt/mini-lightbox.svg)](https://www.npmjs.com/package/mini-lightbox)

> Minimalist image lightbox

## Demo
Check out [the demo page](http://ionicabizau.github.io/mini-lightbox).

## Browser support
As long the [CSS3 transitions](http://caniuse.com/#feat=css-transitions) are supported by your browser, this should work fine. :rocket:
## Examples

### Simple usage

```html
<img id="myImage" src="myImage.png" alt="Some title">
<script>
    new MiniLightbox("#myImage");
</script>
```

### Advanced usage
If you need more stuff (e.g. animations etc), you need to create custom handlers (`customClose` and `customOpen` handlers). Works like a charm with animate.css library. :smile:

```js
function waitForAnimationEnd(element, callback) {
    var animationEnd = "animationend";
    var handleAnimationEnd = function(event) {
      // remove listner
      event.target.removeEventListener(animationEnd, handleAnimationEnd);
      // fire callback
      return callback(event);
    };
    element.addEventListener(animationEnd, handleAnimationEnd);
}

MiniLightbox.customClose = function(self) {
    self.img.classList.add("animated", "fadeOutDown");
    waitForAnimationEnd(self.img, function() {
      self.box.classList.add("animated", "fadeOut");
    });
    waitForAnimationEnd(self.box, function() {
      self.box.classList.remove("animated", "fadeOut", "fadeIn");
      self.img.classList.remove("animated", "fadeOutDown");
      self.box.style.display = "none";
    });
    return false;
};

MiniLightbox.customOpen = function(self) {
    if (self.el.parentElement.tagName === "A") {
      return false;
    }
    self.box.classList.add("animated", "fadeIn");
    self.img.classList.add("animated", "fadeInUp");
};
```

### Using `data-image-opened` attribute
If `data-image-opened` attribute is provided in `img` element, it will be used for the path of the image when the popup is opened.

```html
<img id="myImage" data-image-opened="./big.png" src="small.png" alt="Some title">
```

### Delegation
If images are added dynamically, you need to use delegation:

```js
new MiniLightbox({
    selector: ".content img"
    // the common container where the images are appended
  , delegation: "html"
});
```

## :cloud: Installation


Check out the [`dist`](/dist) directory to download the needed files and include them on your page.

If you're using this module in a CommonJS environment, you can install it from `npm` and `require` it:

```sh
$ npm i --save mini-lightbox
```


## :memo: Documentation


### `MiniLightbox(options)`

Initializes the lightbox according to the options.

**Callbacks**:

The following methods can be used to modify the default behavior:

 - `Minilightbox.customOpen` (Function): If it's a function, it will be
   called then the lightbox is opened. If it returns `false`, the default
   behavior will be prevented.
 - `Minilightbox.customClose` (Function): If it's a function, it will be
   called then the lightbox is closed. If it returns `false`, the default
   behavior will be prevented.

#### Params
- **Object** `options`: An object containing the following fields:
 - `selector` (String): The image query selector.
 - `delegation` (String): The image container where to handle the delegation.

### `close(id)`
Closes the lightboxes.

#### Params
- **String** `id`: The lightbox id. If not provided, it will close all the opened lightboxes.

### `open(id)`
Opens the lightbox. This is called internally.

#### Params
- **String** `id`: The lightbox id.



## :yum: How to contribute
Have an idea? Found a bug? See [how to contribute][contributing].


## :sparkling_heart: Support my projects

I open-source almost everything I can, and I try to reply everyone needing help using these projects. Obviously,
this takes time. You can integrate and use these projects in your applications *for free*! You can even change the source code and redistribute (even resell it).

However, if you get some profit from this or just want to encourage me to continue creating stuff, there are few ways you can do it:

 - Starring and sharing the projects you like :rocket:
 - [![PayPal][badge_paypal]][paypal-donations]—You can make one-time donations via PayPal. I'll probably buy a ~~coffee~~ tea. :tea:
 - [![Support me on Patreon][badge_patreon]][patreon]—Set up a recurring monthly donation and you will get interesting news about what I'm doing (things that I don't share with everyone).
 - **Bitcoin**—You can send me bitcoins at this address (or scanning the code below): `1P9BRsmazNQcuyTxEqveUsnf5CERdq35V6`

    ![](https://i.imgur.com/z6OQI95.png)

Thanks! :heart:


## :dizzy: Where is this library used?
If you are using this library in one of your projects, add it in this list. :sparkles:


 - [`bloggify-lightbox`](https://github.com/Bloggify/lightbox)—MiniLightbox plugin for Bloggify sites

## :scroll: License

[MIT][license] © [Ionică Bizău][website]

[badge_patreon]: http://ionicabizau.github.io/badges/patreon.svg
[badge_amazon]: http://ionicabizau.github.io/badges/amazon.svg
[badge_paypal]: http://ionicabizau.github.io/badges/paypal.svg
[badge_paypal_donate]: http://ionicabizau.github.io/badges/paypal_donate.svg
[patreon]: https://www.patreon.com/ionicabizau
[amazon]: http://amzn.eu/hRo9sIZ
[paypal-donations]: https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=RVXDDLKKLQRJW
[donate-now]: http://i.imgur.com/6cMbHOC.png

[license]: http://showalicense.com/?fullname=Ionic%C4%83%20Biz%C4%83u%20%3Cbizauionica%40gmail.com%3E%20(https%3A%2F%2Fionicabizau.net)&year=2014#license-mit
[website]: https://ionicabizau.net
[contributing]: /CONTRIBUTING.md
[docs]: /DOCUMENTATION.md
