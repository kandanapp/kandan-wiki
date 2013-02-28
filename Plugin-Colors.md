### Description

Plugins to show hex and rgb colors
 
### Usage
Add a hex (i.e: `#fefefe`) or rgb (`rgb(255,255,255)`) to a message

### Output
![ColorPlugin](https://raw.github.com/kandanapp/kandan/resources/ColorPlugin.png)

### Code

#### Hex
```
class Kandan.Plugins.HexColorEmbed
  @options:
    regex: /#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})/g

    template: _.template '''<span class="color-preview" style="background-color:<%= hex %>;"/>'''

  @init: ()->
    Kandan.Modifiers.register @options.regex, (message, state) =>
      for hex in message.content.match(@options.regex)
        replacement = @options.template({hex: hex}) + hex
        message.content = message.content.replace(hex, replacement)

      return Kandan.Helpers.Activities.buildFromMessageTemplate(message)
```

#### RGB
```
class Kandan.Plugins.RgbColorEmbed
  @options:
    regex: /rgb\((\d{1,3}),\s?(\d{1,3}),\s?(\d{1,3})\)/g

    template: _.template '''<span class="color-preview" style="background-color:<%= rgb %>;"/>'''

  @init: ()->
    Kandan.Modifiers.register @options.regex, (message, state) =>
      for rgb in message.content.match(@options.regex)
        replacement = @options.template({rgb: rgb}) + rgb
        message.content = message.content.replace(rgb, replacement)

      return Kandan.Helpers.Activities.buildFromMessageTemplate(message)
```