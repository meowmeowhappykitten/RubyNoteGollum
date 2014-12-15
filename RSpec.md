# General Notes
## What is RSpec?
Test Driven Development

## How to install in a rails project
1.) group :development, :test do
gem 'rspec-rails'
end
2.) bundle install
3.) rails generate rspec:install

##Output and Formatting
--color gives you a more colorful output
--format documentation gives you more organized output
configure block

these can be put in the .rspec file that was originally generated to save time


## Conventions
Tests are often called **specifications**.  **Examples** are given to test a program inside of a specification.  Command example methods:
1. it
2. describe [Class_name or "String"] do
3. include() is used to check that something is part of an array
4. its example: its(:brain) {should be_nil}

An **assertion** states what something "should" be.  Example: zombie.name.should == "Ash"
**Modifier** should, be
**Matcher** <1; checks the number of things: <, have, have(), have_at_least(), have_at_most(), expect{} .to chant {}.by{}, to, not_to, to_not, respond_to(<method_name), be_within(<range>).of(<expected>), exist, satisfy { <block> }, be_kind_of(<class>), be_an_instance_of(<class>)
except can also be used to check if an exception will be raised example: expect {}.to raise_error()
**Pending** important -- denotes that a specification neither passes nor fails.  Useful because you can mark specs as pending in order to test one-by-one.  Can mark as pending by adding "x" before spec, Example: xit or just mark "pending"

# Method
### gem install rspec 
installs rspec
### rspec -- init
to be used in project directory, initializes rspec
### rspec [path/to/specification.rb] 
tests code, can also specific a specific line number to run