# Chapter 4: Creating a new project

Up until now we’ve used the `crystal` command to only run our code.

Actually `crystal` command is pretty useful and does lot more than that. \(check `crystal --help`for more\)

For example we can use it to create a new Crystal project.

```text
$ crystal init app sample
  create  sample/.gitignore
  create  sample/LICENSE
  create  sample/README.md
  create  sample/.travis.yml
  create  sample/shard.yml
  create  sample/src/sample.cr
  create  sample/src/sample/version.cr
  create  sample/spec/spec_helper.cr
  create  sample/spec/sample_spec.cr
Initialized empty Git repository in /Users/serdar/crystal_for_rubyists/code/04/sample/.git/
```

Awesome. `crystal` helped us create a new project. Let’s see what it did for us.

* Created a new folder named sample
* Created a LICENSE
* Created `.travis.yml` to easily integrate Travis for continous integration.
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

Let’s open up `shard.yml`.

```text
name: sample
version: 0.1.0

authors:
  - sdogruyol <dogruyolserdar@gmail.com>

license: MIT
```

This is a default `shard.yml` and it contains the minimal necessary information about our project. Those are

* `name` specifies the name of the project
* `version` specifies the version of the project. Crystal itself uses [semver](http://semver.org/) for version management so it’s a good convention for you to follow.
* `authors` section specifies the authors of the project. By default this is taken from your global `git` configuration.
* `license` specifies the type of your project license. By default this is `MIT`.

Okay. That’s great but what can we do with this `shard.yml`? Well we can use this file to add external libraries\(we call it dependency\) and manage them without even worrying about any folders / paths e.g.. Sweet isn’t it?

Now that we know the true power of `shards` let’s add [Kemal](https://github.com/sdogruyol/kemal) to our `shard.yml` and build a simple web application :\)

Open up `shard.yml`. First we need to add `Kemal` as a dependency to our project. We do this by including

```text
dependencies:
  kemal:
    github: sdogruyol/kemal
    version: 0.14.1
```

That’s great! Now we added `Kemal` to our project. First, we need to install it.

```text
$ shards install
Updating https://github.com/sdogruyol/kemal.git
Updating https://github.com/luislavena/radix.git
Updating https://github.com/jeromegn/kilt.git
Installing kemal (0.14.1)
Installing radix (0.3.0)
Installing kilt (0.3.3)
```

Okay now we are ready to use `Kemal` in our project. Open up `src/sample.cr`

```ruby
require "./sample/*"
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

Now you know how to add dependencies and use others’ `shards` :\)

