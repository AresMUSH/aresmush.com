---
title: Config Validation
description: 
layout: page
tags:
- code
- plugins
- config
---

Most plugins offer configuration options, and it is helpful to make sure the user sets these to sensible values. Otherwise the plugin may behave badly, causing unpredictable results or even game errors.

## Config Check Method

Each plugin has the option to define a `check_config` method in its plugin module file. For example:

    module AresMUSH
      module Who
      ...
        def self.check_config
          validator = WhoConfigValidator.new
          validator.validate
        end
      ...
      end
    end

The internals of this method are entirely up to you.  All you need to do is return either:

* A list of error messages, if there were any problems.
* An empty array if everything was fine.

## Config Validator

Although you can do whatever you want within your `check_config` method, the `ConfigValidator` class makes your life easier.

To start with, you define your own custom validator class. For example, `WhoConfigValidator`.

    module AresMUSH
      module Who
        class WhoConfigValidator
        end
      end
    end

Next we create a copy of the base validator for us to use. The parameter is the name of the configuration section you want to verify. This is the same value you would pass to `Global.read_config(SECTION, ...)`, typically the name of your plugin.

    class WhoConfigValidator
      attr_accessor :validator
      
      def initialize
        @validator = Manage::ConfigValidator.new("who")
      end
    end

Then we implement the `validate` method to perform the actual validation. The ConfigValidator class has a lot of utilities to help us out. These are described further in the next section.  Always end your method with `@validator.errors`. This will return the error list.

    class WhoConfigValidator
    ...
      def validate
        @validator.require_list('who_fields')
        @validator.errors
      end
    end

Finally we use this new class in our `check_config` method, as shown in the example in the previous section.

## Validator Helpers

There are more than a dozen validator helpers in the `ConfigValidator` class.  See the [code](https://github.com/AresMUSH/aresmush/blob/master/plugins/manage/config_validator.rb) for all of them.  A few examples are given below just to show you how it works.

All of these require that you pass in the name of the field. This is the same thing you would pass to `Global.read_config("your_section", FIELD)`.

| `require_text(field)` | The field must be a text string, though it may be empty. |
| `require_nonblank_text(field)` | The field must be a non-blank/empty text string. |
| `require_int(field, min, max)` | The field must be an integer between the specified min/max values (non-inclusive). Either min or max may be nil to omit that check. |
| `check_cron(field)` | Checks to be sure that all the fields of a cron job are valid. |
| `check_channel_exists(field)` | Checks to be sure that the value, if not blank, is actually a chat channel. |

You can have as many validation checks as you want in your `validate` method.  For example:

      @validator.require_boolean('use_advantages')
      @validator.require_nonblank_text('default_linked_attr')
      @validator.require_int('advantages_cost', 1)
      @validator.require_boolean('allow_incapable_action_skills')
      ... it goes on for awhile ...

You can also do your own custom checks by calling `add_error` when something's wrong. For example:

      abilities.each do |name|
        if (FS3Skills.check_ability_name(name))
          @validator.add_error "fs3skills:attributes #{name} cannot contain special characters."
        end
      end

One caveat... if you're going to do advanced checks on hashes and arrays, put them inside a begin/rescue so you don't cause the validator to throw an error if those values are nil.

    # We want to warn them if it's nil
    @validator.require_hash('starting_skills')  
    
    # But also guard ourselves against it being nil.
    begin
      start_skills = Global.read_config('fs3skills', 'starting_skills')
      ...
    rescue Exception => ex
      @validator.add_error "Unknown FS3Skills config error.  Fix other errors first and try again. #{ex} #{ex.backtrace[0]}"
    end




