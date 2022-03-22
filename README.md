# Makefile for a `md` > `pdf` (via `tex`) workflow

A Makefile for compiling Markdown markup to `pdf`. Uses `pandoc` to convert
all the `md` files in your working directory to standalone `tex` files, then
uses `latexmk` to compile those `tex` files to `pdf`.

For many use cases, this is much faster than `pandoc` alone: `latexmk`
generates helper files that help speed along non-initial compilations, and
(unlike `pandoc`) only re-compiles as many times as needed to get
cross-references and citations right. Using `latexmk` also makes it possible
in principle to externalize your `tikz` diagrams.

## Usage

Place `Makefile` in a directory with your `md` file(s). Then, navigate to that
directory with Terminal (or whatever). The following commands are available:

```
$ make                  # Do a basic compilation, using pandoc's latex writer
                        # (and your default.latex template).
```

```
$ make watch            # Watch md files for changes and recompile if needed.
                        # Use control-c to break out.
```

```
$ [cmd] OUT=beamer      # Generate slides, using pandoc's beamer writer (and
                        # your default.beamer template).
```

```
$ [cmd] FLAG=some_flag  # Add a pandoc flag (e.g., --template=custom.tex).
```

```
$ make clean            # Get rid of everything but the md and pdf files.
```

```
$ make debug            # Verbose latexmk compilation that halts on an error.
```

## Dependencies

You'll need `pandoc` and `latexmk`.

If you don't plan on invoking `make watch`, it should work out of the box. If
you want to `make watch`, you'll need
[`fswatch`](https://github.com/emcrisostomo/fswatch). If you're running OS X,
it's easy to install `fswatch` using [Homebrew](http://brew.sh/) (`brew install fswatch`) or
[MacPorts](https://www.macports.org/) (`port install fswatch`).

## Notes

The `aux` files for `latex` and `beamer` can step on each other's toes. If
you're getting strange errors and/or output, try running `make clean`.
