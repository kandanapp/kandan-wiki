### Usage
Type @username

`@gabceb`

### Note

This plugin is also responsible for adding users to the [At Jquery plugin](https://github.com/ichord/At.js)

### Output

![Mentions Plugin](https://raw.github.com/kandanapp/kandan/resources/mentionsPlugin.png)

### Code
```
class Kandan.Plugins.Mentions
  @options:
    regex: /@\S*/g

    template: _.template '''<span class="mention"><%= mention %></span>'''

  @init: ()->
  	Kandan.Data.ActiveUsers.registerCallback "change", (data)=>
      @initUsersMentions(data.extra.active_users)

    Kandan.Modifiers.register @options.regex, (message, state) =>
      for mention in message.content.match(@options.regex)
      	replacement = @options.template({mention: mention})
      	message.content = message.content.replace(mention, replacement)

      return Kandan.Helpers.Activities.buildFromMessageTemplate(message)	
      
  @initUsersMentions: (activeUsers)->
    users = _.map activeUsers, (user)->
      user.username

    $(".chat-input").atwho("@", {data: users});
    return
```