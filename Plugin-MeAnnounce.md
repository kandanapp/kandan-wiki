### Description
Just a very basic plugin for announcements.

### Usage
`/me SOME_ACTION`

`/me Waves`

`/me Dances`

`/me Slaps KandanAdmin with a Trout`

### Code
```
class Kandan.Plugins.MeAnnounce

  @options:
    regex: /^&#x2F;me /

  @init: ()->
    Kandan.Modifiers.register @options.regex, (message, state) =>
      actor = message.user.username || message.user.email
      message.content = message.content.replace @options.regex, "#{actor} "
      return Kandan.Helpers.Activities.buildFromBaseTemplate(message)
```