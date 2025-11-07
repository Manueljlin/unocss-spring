# unocss-spring

A UnoCSS preset that adds spring animations to your project using CSS linear().
Define just two parameters and let the plugin generate the easing curve and the animation duration.


## Parameters

- `spring-bounce-*`
- `spring-duration-*`

Example:

```html
<div class="spring-bounce-60 spring-duration-300 transition-transform hover:scale-150" />
```

Because it's UnoCSS, you can also use arbitrary values without the square braces.

```html
<div class="spring-bounce-65 spring-duration-301 ..." />
```

It's recommended to also use the variant group transformer from UnoCSS since it's more ergonomic to do complex animations. You can also pattern match on data attributes.

```
data-[state='open']:(
  [transition:width_400ms,height_400ms,inset_200ms,transform_400ms]
  w-90dvw
  inset-4 top-unset

  spring-duration-500
  spring-bounce-55
)
data-[state='closed']:(
  [transition:width_300ms,height_150ms,inset_200ms,transform_200ms]
  w-17em active:scale-95
  spring-duration-300
  spring-bounce-20
)
```


## Installation

1. Copy uno-spring-transition.ts into your project.

2. Then, add the preset to your `uno.config.ts` file:

```ts
// uno.config.ts
import { defineConfig, presetMini } from 'unocss'
import { presetSpringTransition } from './uno-spring-transition'

export default defineConfig({
  layers: {
    base:       0,
    components: 1,
    utilities:  2,
    overrides:  99 // add overrides layer so that it has more priority than the default cubic-bezier
  },

  // ...
  
  presets: [
    presetMini(),
    
    // place after your base preset
    presetSpringTransition()
  ]
})
```


## Usage

### `spring-bounce-*`

This class defines the bounce (as a percentage), generates the easing curve, and applies it to the `transition-timing-function`.

- I recommend using low bounce values for most animations unless you want a springy effect.

### `spring-duration-*`

This class defines the perceptual duration of the animation in milliseconds.

- The perceptual duration allows you to intuitively configure the animation, focusing on the most significant part of the motion.

- Since spring easings often have long settling periods, the perceptual duration isn't used as the actual animation duration. Instead, the real duration is calculated based on the `spring-bounce-*` value.


## More Info

The Tailwind version of this plugin, of which this is just an adaptation of, was originally created by [Kevin Grajeda](https://x.com/k_grajeda). The original is open source and available on [GitHub](https://github.com/KevinGrajeda/tailwindcss-spring). I recommend reading his original description for further documentation on the perceptual part of it and so on, it's pretty neat.
