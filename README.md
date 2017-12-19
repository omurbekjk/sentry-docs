# Sentry Documentation

The Sentry documentation is a static site, generated by [Jekyll][jekyll].


## Getting started

You will need [Ruby][ruby], [Bundler][bundler], and [Node.js][nodejs] installed.

```
$ bin/server
```

This will run Bundler to install all the necessary dependencies and then run a webserver at http://localhost:4000/.

[ruby]: https://www.ruby-lang.org/
[bundler]: http://bundler.io/
[nodejs]: https://nodejs.org/


## Layout components

These components make it easier to reproduce markup across the site.

### Language switcher

It is possible to define platform-specific examples of content using `_includes/language_switcher.html`. This is done by capturing content as variables, then passing it to the include. The include first runs the content through the Liquid compiler, then through the Markdown compiler, making it possible to create dynamic, rich styled content.

```
# Define our individual examples
{% capture javascript_example %}
  {%- highlight javascript -%}
  console.log("Hello world")
  {%- endhighlight -%}
{% endcapture %}
{% capture python_example %}
  {%- highlight python -%}
  print("Hello world")
  {%- endhighlight -%}
{% endcapture %}
{% capture ruby_example %}
  {%- highlight ruby -%}
  puts "Hello world"
  {%- endhighlight -%}
{% endcapture %}

# Give ourselves a quick reference to the platforms object
{% assign platforms = site.data.platforms }

# Define an Array of languages to display
{% assign labels = site.Array
  | push: platforms.javascript.name
  | push: platforms.python.name
  | push: platforms.ruby.name
%}

# Define an Array of examples
{% assign examples = site.Array
  | push: javascript_example
  | push: python_example
  | push: ruby_example
%}

# Feed the examples to the component
{% include language_switcher.html
  key="language-switcher-example" # A unique key to identify the switcher
  labels=labels                   # An array of language names
  examples=examples               # An array of content strings
%}
```