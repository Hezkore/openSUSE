# D Language

D is a pretty neat programming language.\
It is a systems programming language with C-like syntax, but with many modern features like garbage collection (optional), contracts, and more.\
And I really like that you can run D code like scripts without needing to compile them first!

D and all the tools we need are available in the package repositories, so we can install them with:
```bash
sudo zypper install dmd dub
```

I'm not sure if we should use `dmd` or `ldc` as the default compiler though.

## New Project

To make a basic _project_ you can just type this in a new folder:
```bash
dub init
```

Edit the `app.d` file in the `source` directory, then compile and run via:
```bash
dub
```

## Quick Script

If you want to run a quick script without creating a project, you can just create an empty text file, like `test.d`.\
Then run it via:
```bash
rdmd test.d
```

## Documentation

If you want a quick tour and introduction to the D language, the [D Language Tour](https://tour.dlang.org/) has got you covered.

If you just want to study the syntax, you can check out the [D Language Reference](https://dlang.org/spec).

And for more information about standard library (awesomely named _Phobos_), check out the [D Language Library Reference](https://dlang.org/phobos/).

## Raylib

I mostly use Raylib with D, which is fairly simple to set up for a new project.

For a new project, you can just run `dub init` like always, and then when it asks `Add dependency` you can just type `raylib-d` to get the latest version.

If you already have a project and want to add Raylib to it, just call:
```bash
dub add raylib-d
```

Once it's added as a dependency, you can download the wrapper library by running:
```bash
dub upgrade
```

And to actually get Raylib itself, you can use the install script that comes with raylib-d:
```bash
dub run raylib-d:install
```

And that's about it!

Here's a simple [Hello World example](https://raw.githubusercontent.com/schveiguy/raylib-d/refs/heads/master/example/source/app.d).\
And here are some of the [Raylib examples in D](https://github.com/schveiguy/raylib-d_examples).