In order to find your unique Bitmoji ID, you need to make sure that you have the Bitmoji chrome extension installed. You also need to make sure that you have a registered account. If you do not have either of these things, please visit the home page for this repository to view the links for getting these things set up.

The way Bitmoji's comic strip rendering server works, you need to provide it with an ID. This ID can be of two different forms. The `bitmoji_avatar_uuid` or the `bitmoji_avatar_id`. Both can be used interchangably when creating comics images, but only one provides control of the [style](https://github.com/matthewnau/libmoji/wiki/Bitmoji-Styles) of the image. In order to provide more functionality, it's best to just obtain the avatar ID rather than the uuid. This guide will show you all the steps for getting your personal ID. Let's start!

# Instructions

1. Browse to the [Bitmoji homepage](https://www.bitmoji.com/). ![Bitmoji homepage](https://imgur.com/j5KWYlL.png)
2. Click the `Log In` button and enter your account information. ![Bitmoji login](https://imgur.com/KvS91pw.png)
3. Click and drag the main `welcome back` image into a new tab. ![Bitmoji new tab](https://imgur.com/ihDZ8bV.png)
4. Copy the URL of the image, and pass it to the `getAvatarId` function in Libmoji. This will return your unique `bitmoji_avatar_id` as a string. 
```JavaScript
console.log(libmoji.getAvatarId("https://render.bitstrips.com/v2/cpanel/8968038-316830037_35-s5-v1.png?transparent=1&palette=1"));
/* returns 316830037_35-s5 */
```
5. Ta-da! You now have your ID. Use it to generate all the comics that your heart desires! It's also worth noting, if you look more closely at the `bitmoji_avatar_id`, it cotains the string `s5`. This portion determines which style of avatar you want to use. (1, 4, or 5) you can manually change this to modify what the comic will look like. The `uuid` does NOT allow this feature because it is a hashed version of the normal id. So when manipulating a comic, its best to use the standard ID.

6. If for some reason you wanted to find your `bitmoji_avatar_uuid`, you will be able to find it saved in a cookie on the Bitmoji website. Your `bitmoji_avatar_id` is also saved here, this method is just a little more complex in my opinion. ![Bitmoji cookies](https://imgur.com/UliOr0y.png)