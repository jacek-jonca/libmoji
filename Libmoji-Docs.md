Here you can find a list of all functions and variables that are available to use with Libmoji, and what they do. You will also find descriptions and example code for each of the following.

### `genders`
An array that contains the string and index value associated with each gender.
```JavaScript
const genders = [['male',1],["female",2]];
```

### `poses`
A string array that contains all possible poses that can be passed to the `buildUrl` method.
```JavaScript
const poses = ["fashion","head","body"];
```

### `styles`
An array that contains the string and index value associated with each style.
```JavaScript
const styles = [["bitstrips",1],['bitmoji',4],["cm",5]];
/* bitstrips, Bitmoji classic, Bitmoji deluxe */
```

### `basePreviewUrl`
A string which contains the beginning of every preview engine image's URL.
```JavaScript
const basePreviewUrl = "https://preview.bitmoji.com/avatar-builder-v3/preview/";
```

### `baseCpanelUrl`
A string which contains the beginning of every cpanel engine image's URL.
```JavaScript
const baseCpanelUrl = "https://render.bitstrips.com/v2/cpanel/";
```

### `baseRenderUrl`
A string which contains the beginning of every render engine image's URL.
```JavaScript
const baseRenderUrl = "https://render.bitstrips.com/render/";
```

### `getTraits(gender, style)`
Takes `gender` and `style` strings as input and returns a `traits` object with a list of all possible traits for a specific gender and style.
```JavaScript
console.log(libmoji.getTraits("male"));
/* returns an array of trait objects */
```

### `getBrands(gender)`
Takes a `gender` string as input and returns a `brands` object with a list of all possible brands for a specific gender.
```JavaScript
console.log(libmoji.getBrands("male"));
/* returns an array of brand objects */
```

### `getOutfits(brand)`
Takes a `brand` object as input and returns an `outfits` object with a list of all possible outfits for a specific brand.
```JavaScript
console.log(libmoji.getOutfits(libmoji.getBrands("male")[0]));
/* returns an array of outfit objects from the first male brand */
```

### `getValues(trait)`
Takes a `trait` object as input and returns a `values` object with a list of all possible values for a specific trait.
```JavaScript
console.log(libmoji.getValues(libmoji.getTraits("male")[0]));
/* returns an array of values for the first male trait */
```

### `getKey(trait)`
Takes a `trait` object as input and returns its name as a `string`.
```JavaScript
console.log(libmoji.getKey(libmoji.getTraits("male")[0]));
/* console would print "beard" since it is the first male trait */
```

### `getAvatarUuid(url)`
Takes an image `url` string as input and returns the avatar uuid associated with it as a `string`.
```JavaScript
console.log(libmoji.getAvatarUuid(https://render.bitstrips.com/v2/cpanel/f3b1c198-8c3a-4386-a2de-5902bf7309df-be541d0a-5344-47a3-94ac-5e3912651ea5-v1.png?transparent=1&palette=1));
/* console would print 'be541d0a-5344-47a3-94ac-5e3912651ea5' */
```

### `getAvatarId(url)`
Takes an image `url` string as input and returns the avatar id associated with it as a `string`.
```JavaScript
console.log(libmoji.getAvatarId(https://render.bitstrips.com/v2/cpanel/8968038-316830037_35-s5-v1.png?transparent=1&palette=1));
/* console would print '316830037_35-s5' */
```

### `getComicId(template)`
Takes a `template` object as input and returns the comic id associated with it as a `string`.
```JavaScript
console.log(libmoji.getComicId(libmoji.randTemplate(libmoji.templates)));
/* console would print a comic id */
```

### `randInt(max)`
Takes a `max` `integer` as input and returns a random `integer`. The pool of values starts at 0 (included) and ends at the max. (excluded) The random value can never be the max, at most it will be 1 less since the array index starts at 0.
```JavaScript
console.log(randInt(2));
/* console would either print '1' or '0' */
```

### `randBrand(brands)`
Takes a `brands` object as input and returns a random `brand` object.
```JavaScript
console.log(libmoji.randBrand(libmoji.getBrands("male")));
/* console would print a random brand object from the list of male brands */
```

### `randOutfit(outfits)`
Takes an `outfits` object as input and returns a random outfit `string`.
```JavaScript
console.log(libmoji.randOutfit(libmoji.getOutfits(libmoji.randBrand(libmoji.getBrands("male")))));
/* console would print a random male outfit */
```

### `randValue(trait)`
Takes a `trait` object as input and returns a random value `string`.
```JavaScript
console.log(libmoji.randValue(libmoji.getTraits("male")[0]));
/* console would print a random value taken from the first male trait value pool */
```

### `randTraits(traits)`
Takes a `traits` object as input and returns a `traits` object. Every trait has a random value assigned. The returned `traits` object consists of key/value pairs and does not just list traits (like the input).
```JavaScript
console.log(libmoji.randTraits(libmoji.getTraits("male")));
/* console would print a male traits object with random values */
```

### `mapTraits(traits)`
Takes a `traits` object (key/value form) as input and returns a `string`. This function is only used by `buildUrl` to convert a traits object to string form for the URL.
```JavaScript
console.log(libmoji.mapTraits(libmoji.randTraits(libmoji.getTraits("male"))));
/* console would print a string of traits to be used in a url */
```

### `randTemplate(templates)`
Takes a `templates` object as input and returns a `template` object.
```JavaScript
console.log(libmoji.randTemplate(libmoji.templates));
/* console would print a template object */
```

### `buildPreviewUrl(pose, scale, gender, style, rotation, traits, outfit)`
This function requires a pose (`string`), scale (`integer`), gender (`integer`), style (`integer`), rotation (`integer`), traits (key/value `traits` object), and an outfit (`string`). Returns a URL `string`.
```JavaScript
let gender = libmoji.genders[libmoji.randInt(2)];
let style = libmoji.styles[libmoji.randInt(3)];
let traits = libmoji.randTraits(libmoji.getTraits(gender[0],style[0]));
let outfit = libmoji.randOutfit(libmoji.getOutfits(libmoji.randBrand(libmoji.getBrands(gender[0]))));

console.log(libmoji.buildPreviewUrl("fashion",3,gender[1],style[1],0,traits,outfit));
/* console would print a random image url */
```

### `buildCpanelUrl(comicId, avatarId, transparent, scale)`
This function requires a comic id (`string`), avatar id or uuid (`string`), transparent (`integer`), and a scale (`integer`). Returns a URL `string`.
```JavaScript
let comicId = libmoji.getComicId(libmoji.randTemplate(libmoji.templates));
let avatarId = libmoji.getAvatarId(https://render.bitstrips.com/v2/cpanel/8968038-316830037_35-s5-v1.png?transparent=1&palette=1);

console.log(libmoji.buildCpanelUrl(comicId,avatarId,1,2));
/* console would print a random image url with your Bitmoji */
```

### `buildRenderUrl(comicId, avatarId, transparent, scale)`
This function requires a comic id (`string`), avatar id or uuid (`string`), transparent (`integer`), scale (`integer`), and an outfit (`string`). Returns a URL `string`.
```JavaScript
let comicId = libmoji.getComicId(libmoji.randTemplate(libmoji.templates));
let avatarId = libmoji.getAvatarId(https://render.bitstrips.com/v2/cpanel/8968038-316830037_35-s5-v1.png?transparent=1&palette=1);
let outfit = libmoji.randOutfit(libmoji.getOutfits(libmoji.randBrand(libmoji.getBrands("male"))));

console.log(libmoji.buildRenderUrl(comicId,avatarId,1,2,outfit));
/* console would print a random image url with your Bitmoji */
```