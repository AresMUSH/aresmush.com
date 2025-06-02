---
title: Templates
description: 
layout: page
tags:
- code
- templates
---

Templates are a special code class that handle complex information display.  There are templates for all sorts of things in the game:  the who/where list, mail messages, forums, character sheets, profile, descriptions and more.

{% include toc.html %}

## The Template Engine

A template consists of two parts:

1. The **Template Renderer**, which sets up the template and contains methods to help format everything.
2. The **ERB Template**, which uses Ruby's [ERB Template system](https://github.com/ruby/erb) to mingle text with embedded Ruby code to control the actual display. (Similar to embedded Python for those familiar with that.)

{% tip %} 
Template files are located in a 'templates' folder within each plugin - for example `aresmush/plugins/describe/templates/character.erb`.
{% endtip %}

For example, here is a sample of the ERB file for the character description template:

```text
<%= header %>
%xh<%= char.name %>%xn
<%= military_name(char) %>
<%= divider %>
<%= char.description %>
<%= divider %>
<%= footer %>
```

{% tip %} 
Anything inside `<%= %>` brackets is evaluated as code by the template engine.
{% endtip %}

Here's what that would look like in a MU client:

```text
+==~~~~~====~~~~====~~~~====~~~~=====~~~~=====~~~~====~~~~====~~~~====~~~~~==+
Stirling
Major Nyssa "Whisper" Stirling
------------------------------------------------------------------------------
Fiery red hair falls down past this woman's shoulders, usually bound in a sensible braid. Her average height and lithe build aren't very remarkable, but they belie a well-toned muscular form. She's wearing standard-issue green fatigues, the pins showing a rank of Major.
+==~~~~~====~~~~====~~~~====~~~~=====~~~~=====~~~~====~~~~====~~~~====~~~~~==+
```

And here is a snippet of the template renderer class.

```ruby
class CharacterTemplate < ErbTemplateRenderer
  attr_accessor :char
  def initialize(char)
    @char = char
    super File.dirname(__FILE__) + "/character.erb"        
  end
  
  # Fullname with rank and callsign, if set.  (e.g. Commander William "Husker" Adama)
  def military_name(char)
    Ranks.military_name(char)
  end
end
```

Notice how it provides the 'char' accessor so the template can do things like `<%= char.name %>`.  It also provides the military name helper to enable `<%= military_name(char) %>`.

{% tip %} 
You <i>can</i> put code directly into the ERB file, but it gets very messy very quickly.  It's often best to leave anything complicated into a helper.
{% endtip %}

## Using Templates

To use a template, you simply instantiate the renderer class and call the render method.  For example:

        template = WhoTemplate.new online_chars
        client.emit template.render

Many renderers expect some parameters passed in - a character, a room, or - in this case - the list of characters who are currently online.  Templates handle _how_ to display data, but other code should figure out _what_ to show.

### Common Templates

Ares provides a few common templates in the Globals plugin that are used everywhere.  The two most common are `BorderedDisplayTemplate` and `BorderedListTemplate`:

```text
    ------------------------------
              Title
              SubTitle
    Text
    SubFooter
    ------------------------------
```

{% tip %} 
Everything except the text/list is optional, so you can customize the display as desired.
{% endtip %}

There's also a table, a line with text in the middle, and a standard page footer for multi-page commands.  See the code in `aresmush/plugins/globals/templates` for details.

## Customizing Templates

A few templates will automatically be customized based on your game configuration.  The 'who' template lets you pick fields and the 'profile' template automatically shows whatever demographics you've configured.

You can customize other templates too - it just requires you to change the template code - either the ERB or the template renderer, or both.

For example, if you don't like showing the "military name" stuff on descs and want to show some basic demographics instead, you could modify the ERB template like so:

```text
<%= header %>
%xh<%= char.name %>%xn
<%= char.age %> year old <%= gender(char) %> with <%= hair(char) %> hair
<%= divider %>
<%= char.description %>
<%= footer %>
```

And then add gender and hair helpers to the template renderer:

    class CharacterTemplate < ErbTemplateRenderer
      ...
      def gender(char)
        Demographics.gender_noun(char)
      end
      def hair(char)
        char.demographic(:hair) || "no"
      end
    end

## Creating a Template

To create your own new template, here are the pieces you need:

Create the ERB file. (e.g. plugins/custom/templates/foo.erb)

```text
This is my template. Hello <%= char.name %>
```

Create the template renderer.  (e.g. plugins/custom/templates/foo_template.rb)

    class FooTemplate < ErbTemplateRenderer
      attr_accessor :char 
      
      def initialize(char)
        @char = char
        super File.dirname(__FILE__) + "/foo.erb"        
      end

Use the template

    template = FooTemplate.new(enactor)
    client.emit template.render

{% tip %} 
In this example, our template needs only a single character, but other templates may need other parameters.  Just make sure that the list you define in your template renderer's initialize method matches what you pass in the `new` call when you create it.
{% endtip %}

## Common Formatting Helpers

All template renderers have some common formatting helpers available.

* header - Header line, aka %lh (`<%= header %>`)
* footer - Footer line, aka %lf (`<%= footer %>`)
* divider - Divider line, aka %ld (`<%= divider %>`)
* left - Left-justifies and trims text (`<%= left(text, width, padding_char) %>`)
* right - Right-justifies and trims text (`<%= right(text, width, padding_char) %>`)
* center - Center-justifies and trims text (`<%= center(text, width, padding_char) %>`)

{% tip %} 
The padding char is optional in left/right/center, and defaults to a space.
{% endtip %}

Some of the template renderers share common helpers with another template.  You'll see this when the renderer has a line like  `include CharDescTemplateFields`  near the top of the file.  For example, the description and glance templates share some helpers from  `plugins/describe/char_desc_template_fields.rb` .  

{% tip %} 
If you don't see the helper you're looking for in the template renderer, look for a shared helper file.
{% endtip %}

## The One-Line Trick

ERB Templates take linebreaks literally.  If text appears on a different line in the template file, it'll show up on a different line on the screen.

The only trouble is that sometimes MUSHes have a lot of different fields on one line of the screen - like a who list with six columns.  If you tried to jam the code for every column into one line of the template, it would be really ugly.

Fortunately there's an ERB trick for this.  If you end a line with a field like `<% -%>` instead of `<% %>`, then there won't be a linebreak displayed between those two lines.

For example: 
 
    <% chars.each do |c| %>
    <%= status_color(c) %><%= left( status(c), 7 ) %><%= "%xn" -%>
    <%= left( c.name, 23 ) -%>
    <%= left( department(c), 20 ) -%>
    <% end >

The status, name and department fields will all appear on the same line.