In order to build a Bitmoji, it's important to understand what components comprise the URL. For this example, we will examine the URL for the first image above. The following URL is what generated [this](https://preview.bitmoji.com/avatar-builder-v3/preview/head?scale=3&gender=1&style=5&rotation=0&beard=2212&brow=1555&cheek_details=1356&ear=1423&eye=1614&eyelash=-1&eye_details=1352&face_lines=1366&glasses=2465&hair=1723&hat=2495&jaw=1400&mouth=2338&nose=1482&beard_tone=8678208&blush_tone=16754088&brow_tone=6772090&eyeshadow_tone=-1&hair_tone=8637550&hair_treatment_tone=10513945&lipstick_tone=16740668&pupil_tone=5793385&skin_tone=9657655&body=1&face_proportion=13&eye_spacing=0&eye_size=2&outfit=990491) image.

```
https://preview.bitmoji.com/avatar-builder-v3/preview/head?scale=3&gender=1&style=5&rotation=0&beard=2212&brow=1555&cheek_details=1356&ear=1423&eye=1614&eyelash=-1&eye_details=1352&face_lines=1366&glasses=2465&hair=1723&hat=2495&jaw=1400&mouth=2338&nose=1482&beard_tone=8678208&blush_tone=16754088&brow_tone=6772090&eyeshadow_tone=-1&hair_tone=8637550&hair_treatment_tone=10513945&lipstick_tone=16740668&pupil_tone=5793385&skin_tone=9657655&body=1&face_proportion=13&eye_spacing=0&eye_size=2&outfit=990491
```

This URL may look complex at first glance, but all it really does is combine many small pieces of information that describe how the image should look. Let's examine what all goes into the URL by using the following table.

| Component | Description |
| --- | --- |
| `https://preview.bitmoji.com/avatar-builder-v3/preview/` | This is the base URL. All image URLs will begin with this. |
| `head` | This describes what pose the image should use. In the example, the image appears to only show the head. |
| `?scale=` | This describes how large the image should be rendered. Images are rendered as PNGs, and the larger the scale, the higher the resolution of the image. |
| `&gender=` | Describes which gender the avatar should be. This determines what traits to load, and which outfits are available. |
| `&style=` | This determines which avatar style to render. This must be used in conjunction with the correct trait list for a style. |
| `&rotation=` | Determines which way the avatar faces. It only works on `body` and `head` poses. |
| `&beard=2212`, `&brow=1555`, ... `&skin_tone=9657655`, `&body=1`, `&face_proportion=13`, `&eye_spacing=0`, `&eye_size=2` | This is where all gender specific traits are injected into the URL. Not all traits are required to render, and every trait has a specific set of values that work with it. For any trait that has `tone` in its name, its value is actually just a color in decimal form. |
| `&outfit=` | This is the outfit that the Bitmoji is wearing. The outfit parameter is not required, and will render in blank white clothes otherwise. |

All of these parameters can be changed to create a Bitmoji of your preference. To find a complete list of all possible traits and values for a specific gender, consult the `assets.json` file, or print a list using the functions provided by Libmoji.