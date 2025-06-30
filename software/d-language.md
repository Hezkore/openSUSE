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