# Rendering Engines

Bitmoji is a large and complex service which employs multiple APIs in an effort to render images to the end user. Libmoji tries to make it possible to access these APIs in every way possible. It appears that different rendering engines are used for different components of the Bitmoji platform. The engines will be known respectively as the `preview`, `cpanel`, and `render` engines. This article will explore in depth the capabilities and limitations associated with each in an effort to provide you with enough information to successfully utilize Libmoji.

---

# The Preview Engine

The preview engine is used for displaying what the user's avatar will look like before it is saved to Bitmoji's database. This allows the user to mix and match combinations of physical traits, outfits, and accessories. All preview images start with the base URL of `https://preview.bitmoji.com/avatar-builder-v3/preview/`. The preview engine allows for customization of all aspects of a Bitmoji. Read [this article](https://github.com/matthewnau/libmoji/wiki/Understanding-Bitmoji) to understand what elements comprise preview image URLs.

The preview engine has the ability to render many aspects of an avatar, but it does not allow for the use of comics. Comics are the part of Bitmoji that consumers use on a daily basis. Unfortunately, in order to utilize the comics feature an account must be held with either Bitmoji or Snapchat.

<p align="center">
<img height="300px" src="https://preview.bitmoji.com/avatar-builder-v3/preview/body?scale=3&gender=2&style=1&rotation=0&brow=130&cheek_details=644&ear=260&earring=511&eye=155&eyelash=313&eye_details=254&face_lines=274&glasses=475&hair=255&hat=26&jaw=287&mouth=195&nose=621&pupil=222&blush_tone=14904417&brow_tone=14386178&eyeshadow_tone=6857137&hair_tone=8667546&lipstick_tone=6946830&pupil_tone=11767108&skin_tone=14664067&body=7&breast=1&face_proportion=6&outfit=889514"/>
<img height="300px" src="https://preview.bitmoji.com/avatar-builder-v3/preview/body?scale=3&gender=2&style=4&rotation=0&brow=766&cheek_details=998&eyelash=-1&eye_details=935&face_lines=-1&glasses=965&hair=1058&hat=1198&mouth=1056&nose=1031&blush_tone=16754890&brow_tone=14386178&eyeshadow_tone=2698284&hair_tone=11093553&lipstick_tone=16693913&pupil_tone=11767108&skin_tone=15257000&body=8&breast=0&face_proportion=8&outfit=1018470"/>
<img height="300px" src="https://preview.bitmoji.com/avatar-builder-v3/preview/body?scale=3&gender=2&style=5&rotation=0&brow=1574&cheek_details=-1&ear=1434&eye=1613&eyelash=-1&eye_details=-1&face_lines=1359&glasses=2435&hair=1669&hat=2505&jaw=1410&mouth=2340&nose=1504&blush_tone=11253434&brow_tone=152522&eyeshadow_tone=10895167&hair_tone=8667546&hair_treatment_tone=16711608&lipstick_tone=1084817&pupil_tone=8404014&skin_tone=5451546&body=9&breast=0&face_proportion=1&eye_spacing=2&eye_size=0&outfit=997997"/>
</p>

---

# The Cpanel Engine

The cpanel engine is one of the 2 engines used for rendering what Bitmoji comics should look like. Of the 2, the cpanel engine offers the least amount of customization and offers no known benefits over the alternative. Despite its lackluster feature count, I still chose to include the functionality in Libmoji so that any information I uncovered would be accessible to the public. 

All cpanel URLs start with `https://render.bitstrips.com/v2/cpanel/`. The cpanel engine only provides modification access for parameters such as `transparent` (0 or 1), `scale` (1 or 2), and allows the style of the avatar to be changed. I uncovered the additional parameter `palette`, which has a default value of 1. Changing this value does not appear to do anything, and the parameter can even be omitted entirely.

<p align="center">
<img height="200px" src="https://render.bitstrips.com/v2/cpanel/f3b1c198-8c3a-4386-a2de-5902bf7309df-be541d0a-5344-47a3-94ac-5e3912651ea5-v1.png?transparent=1&palette=1&scale=2"/>
</p>

---

# The Render Engine

The render engine is probably the most customizable of all the preview engines, but how it operates is largely hidden. Bitmoji recently deprecated their online avatar editor, and only allows you to edit your personal avatar from their app. The old editors values and engine can still be accessed, but it makes it hard to find any new information on it. When viewing the traffic while building an avatar, its clear that the preview engine was meant to replace this section of the avatar-building process.

This engine provides a ton of flexibility when creating an image URL. It has a base URL of `https://render.bitstrips.com/render/`.  It has the same parameters as the cpanel engine, except it allows even more parameters. There is a `sex` paramter with options 1or 2. (Same as the gender in Libmoji) One notable difference of this engine is the `pd2` parameter. You can directly modify the physical traits of a Bitmoji on top of the comic that is being rendered. You have to supply your ID, but anything after that overrides your original Bitmoji! Here is an example of the pd2 parameter being used.

```
pd2={"cranium":"cranium_bm35","forehead":"forehead_bm1"}
```

This directly overrides the `cranium` and `forehead` traits of your Bitmoji. These traits are from the legacy system and do not work in the preview engine. The render engine can load `Bitmoji Deluxe` avatars, but does not have access to the new traits because they have a numbering system, and not an attribute label. To find all legacy data, I have provided a [legacy.json](https://github.com/matthewnau/libmoji/blob/master/json/legacy.json) file with all traits and values that i was able to record before the editor was deprecated. Although new traits do not work with the render engine, all outfits from the templates file do appear to work.

Bitmoji colors are modified in the same way pd2 is. With the paramter `colours={"ff9866":9476876}`. Every new color/key combo is separated by a comma like pd2 as well. What makes this difficult is the color labels correspond to a random trait color. Some experimentation will need to be done in order to find what `ff9866` is changing the color of an etc.

Surprisingly, this isn't even all we have access to change. There is a `proportion` parameter. (supply it with an integer value) This determines the face/head shape. One of the most useful parameters is `cropped`. Modifiying this value can render a Bitmoji in the pose of a specific comic, but without the actual comic-related images! When using the render engine, all comic features are cropped out by default, but whitespace is still left in its place. To render comics, you will unfortunately have to use the cpanel engine. You can specify `cropped` to `head` or `body` to remove whitespace. Look at the example of the cpanel vs the render engine below.

<p align="center">
<img height="300px" src="https://render.bitstrips.com/v2/cpanel/31f20050-0209-4c06-86c3-7cce3a640d39-be541d0a-5344-47a3-94ac-5e3912651ea5-v1.png?transparent=1&palette=1&scale=2"/>
<img height="300px" src="https://render.bitstrips.com/render/31f20050-0209-4c06-86c3-7cce3a640d39/be541d0a-5344-47a3-94ac-5e3912651ea5-v1.png?transparent=1&palette=1&scale=4"/>
</p>

The cpanel and render engines sometimes can prove unpredictable, so if you don't need comic functionality, it may be best to stick with the preview engine. If you need avatar control, go with the preview engine. If you need comics, use cpanel. And if you want to render your personal Bitmoji in different positions, use the render engine. Good luck!