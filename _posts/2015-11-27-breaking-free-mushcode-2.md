---
title: Breaking Free from MUSHCode - Part 2
date: '2015-11-27'
layout: post
description:
categories:
tags: [feature, code]
author: Faraday
preview_image: mushcode2.jpg
teaser: Ares' alternative to MUSH softcode.
---

In the <a href="/posts/breaking-free-from-mushcode-part-1/">previous article</a>, I talked about some of the downsides of MUSHCode. This time I'll explain how AresMUSH offers a different way to code.

<h1>A Gem of a Language</h1>

All of Ares is written in Ruby, a common programming language. This means:

<ul>
<li>It's easier to learn.  There's a great interactive tutorial at <a href="http://tryruby.org/levels/1/challenges/0">tryruby.org</a>, and thousands of books and articles on the subject.  Ruby is not a big leap for anyone who's programmed in another language.</li>
<li>It's easier to get help.  There are places like <a href="http://stackoverflow.com">StackOverflow</a> to ask questions, and you're way more likely to find someone who knows Ruby than one who knows MUSHCode.</li>
<li>It's easier to maintain.  Ruby code is way more intuitive and easier to read than MUSHCode.</li>
</ul>

<h1>Plug and Play</h1>

While older MUSH servers have hardcode and softcode, AresMUSH has the <strong>Engine</strong> and the <strong>Plugins</strong>. The Engine is the backbone of the game. It handles player connections, command dispatching, configuration, and a few other central responsibilities. You <em>can</em> change the Engine code, but you shouldn't need to.

Most of the game systems - even basic things like movement and descriptions - are implemented as Plugins. Plugins are designed to be flexible. You can easily add, change or remove a Plugin - even while the game is running!

Need to restrict movement during combat? Just modify the Movement Plugin. Want to use a custom channel system? Just replace the Channels Plugin with your own.

Because you can modify the Plugins directly, you don’t end up with a hardcoded “who” and a softcoded “+who” on top of it.

Here are just a few of the Plugins that come with every Ares install out of the box:

<ul>
<li>Posing and Pages</li>
<li>Rooms and Movement</li>
<li>Who / Where</li>
<li>Bulletin Boards</li>
<li>Channels</li>
<li>FS3 Skills, Chargen and Combat</li>
<li>and more</li>
</ul>

<h1>A Closer Look</h1>

What does Ares code look like?  Here are some snippets from the multi-descer command that creates an outfit.

Each command has its own command handler, which must tell the dispatcher which commands it wants.  This one wants the "outfit/set" command.

      def want_command?(client, cmd)
        cmd.root_is?(&quot;outfit&quot;) &amp;amp;&amp;amp; cmd.switch_is?(&quot;set&quot;)
      end

The dispatcher will automatically call any error checks you define in your command handler.  If one of them returns an error message, the dispatcher will stop trying to process the command and display that error to the user.

Here's an example of an error check that makes sure the player is logged into a character (and not just sitting on the login screen):

       def check_for_login
          return t('dispatcher.must_be_logged_in') if !client.logged_in?
          return nil
       end

Checking for login is one of several common error checks that can be included with a single line of code so you don't have to copy/paste the code everywhere.

    include CommandRequiresLogin

Most commands interact with the database and send messages back to the player.  The <strong>client</strong> object represents the connection with the player's MUSH client. If the player is logged into a character, <strong>client.char</strong> will let you access that character object.

Here's how the "outfit/set" command stores the outfit to the character and tells the player about it:

      def handle
        client.char.outfits[self.name] = self.desc
        client.char.save!
        client.emit_success t('describe.outfit_set')
      end

More details about plugins and command handling will be given in future blog posts and in the forthcoming tutorials.

<h1>Up Next</h1>

In the final article of this series, we'll take a look at the mechanics behind actually editing the code.