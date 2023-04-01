# Chapter 4: Creating a new project

Up until now we’ve used the `crystal` command to only run our code.

Actually `crystal` command is pretty useful and does lot more than that. \(check `crystal --help`for more\)

For example we can use it to create a new Crystal project.

```text
$ crystal init app sample
  create  sample/.gitignore
  create  sample/.editorconfig
  create  sample/LICENSE
  create  sample/README.md
  create  sample/shard.yml
  create  sample/src/sample.cr
  create  sample/spec/spec_helper.cr
  create  sample/spec/sample_spec.cr
Initialized empty Git repository in /Users/serdar/crystal_for_rubyists/code/04/sample/.git/
```

Awesome. `crystal` helped us create a new project. Let’s see what it did for us.

* Created a new folder named sample
* Created a LICENSE
* Created `shard.yml` for dependency management.
* Initialized an empty Git repository
* Created a README for our project
* Created `src` and `spec` folders to put our code and tests\(ssh..we’ll talk about it soon\) in it.

Let’s run it.

```text
$ cd sample
$ crystal src/sample.cr
```

Nothing! Yay :\)

Now that we create our first project. Let’s use some external libraries.

## Using Shards for dependency management  <a id="using-shards-for-dependency-management"></a>

To manage dependencies of a project we use `shards`. `shards` is like `bundler` and `shard.yml` is like `Gemfile`.

* [awesome-crystal](https://github.com/veelenga/awesome-crystal) has a curated list of Crystal shards.
* [crystalshards.org](https://crystalshards.org/) lists all of the available Crystal shards on GitHub (similar to rubygems.org)
* [Here is a list of some popular Ruby gems that have been ported to Crystal](https://github.com/crystal-lang/crystal/wiki/Crystal-Shards-for-Ruby-Gems).

Let’s open up `shard.yml`.

```text
name: sample
version: 0.1.0

authors:
  - sdogruyol <dogruyolserdar@gmail.com>

targets:
  sample:
    main: src/sample.cr

crystal: 1.5.0

license: MIT
```

This is a default `shard.yml` and it contains the minimal necessary information about our project. Those are

* `name` specifies the name of the project
* `version` specifies the version of the project. Crystal itself uses [semver](http://semver.org/) for version management so it’s a good convention for you to follow.
* `authors` section specifies the authors of the project. By default this is taken from your global `git` configuration.
* `crystal` specifies the version of Crystal that the project is using.
* `license` specifies the type of your project license. By default this is `MIT`.

Okay. That’s great but what can we do with this `shard.yml`? Well we can use this file to add external libraries\(we call it dependency\) and manage them without even worrying about any folders / paths e.g.. Sweet isn’t it?

Now that we know the true power of `shards` let’s add [Kemal](https://github.com/kemalcr/kemal) to our `shard.yml` and build a simple web application :\)

Open up `shard.yml`. First we need to add `Kemal` as a dependency to our project. We do this by including

```text
dependencies:
  kemal:
    github: kemalcr/kemal
    version: 1.2.0
```

That’s great! Now we added `Kemal` to our project. First, we need to install it.

```text
$ shards install
Resolving dependencies
Fetching https://github.com/kemalcr/kemal.git
Fetching https://github.com/luislavena/radix.git
Fetching https://github.com/crystal-loot/exception_page.git
Fetching https://github.com/sija/backtracer.cr.git
Installing radix (0.4.1)
Installing backtracer (1.2.1)
Installing exception_page (0.2.2)
Installing kemal (1.2.0)
Writing shard.lock
```

Okay now we are ready to use `Kemal` in our project. Open up `src/sample.cr`

```ruby
require "kemal"

module Sample

  get "/" do
    "Hello World!"
  end

end

Kemal.run
```

Look how we used `require` to access `Kemal` in our program.

Let’s run.

```text
$ crystal src/sample.cr
[development] Kemal is ready to lead at http://0.0.0.0:3000
```

Go to `localhost:3000` and see it in action!

Now you know how to add dependencies and use others’ `shard`s :\)
