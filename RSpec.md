# General Notes
## What is RSpec?
Test Driven Development

## How to install in a rails project
1. group :development, :test do
2. gem 'rspec-rails'
3. end
4. bundle install
5. rails generate rspec:install


##Output and Formatting
--color gives you a more colorful output
--format documentation gives you more organized output
configure block

these can be put in the .rspec file that was originally generated to save time


## Conventions
Tests are often called **specifications**.  **Examples** are given to test a program inside of a specification.  Command example methods:
1.  it
2.  describe [Class_name or "String"] do
3. include() is used to check that something is part of an array
4. its example: its(:brain) {should be_nil}


An **assertion** states what something "should" be.  Example: zombie.name.should == "Ash"

**Modifier** should, be

**Matcher** <1; checks the number of things: <, have, have(), have_at_least(), have_at_most(), expect{} .to chant {}.by{}, to, not_to, to_not, respond_to(<method_name), be_within(<range>).of(<expected>), exist, satisfy { <block> }, be_kind_of(<class>), be_an_instance_of(<class>)
except can also be used to check if an exception will be raised example: expect {}.to raise_error()

**Pending** important -- denotes that a specification neither passes nor fails.  Useful because you can mark specs as pending in order to test one-by-one.  Can mark as pending by adding "x" before spec, Example: xit or just mark "pending"

**Hooks** Specify code that should run before and/or after each example
before {:each} runs before each example, can also run before{:all} could also run after{:each} or after{:all}

**Filters** You can tag each it or context blocks with a filter at end of line, Example vegan: true tags as vegan, when running rspec in bash, you can choose to run only certain tags, or can put in spec_helper configure block.  Tip:  you can tag slow examples, so that you don't have to run them every time.

**Stub** For replacing a method with code that returns a specified result, basically blanks out specified method in default

**Mock** a stub with an expectation attached to it.  Example: zombie.weapon.should_recieve(:slice)  stubs out slice method and makes expectation that it is called

# Method
### gem install rspec 
installs rspec
### rspec -- init
to be used in project directory, initializes rspec
### rspec [path/to/specification.rb] 
tests code, can also specific a specific line number to run, you can run specific tags by using --tag or exclude certain tags with --tag ~