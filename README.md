Lambdapi, a proof assistant based on the λΠ-calculus modulo rewriting
=====================================================================

Lambdapi is a proof assistant based on the λΠ-calculus modulo rewriting,
mostly compatible with the proof checker Dedukti. More details are given
in the [documentation](doc/DOCUMENTATION.md).

[![Gitter](https://badges.gitter.im/deducteam-dedukti/lambdapi.svg)](https://gitter.im/deducteam-dedukti/lambdapi?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

Installation via [Opam](http://opam.ocaml.org/)
---------------------

We will only publish a new version of `lambdapi` Opam package when the
development has reached a more stable test. For now, we advise you to
pin the development repository to get the latest bug fixes.

```bash
opam pin add lambdapi https://github.com/Deducteam/lambdapi.git
```
Dependencies and compilation
----------------------------

Lambdapi requires a Unix-like system. It should work on Linux as well as on
MacOS. It might also be possible to make it work on Windows with Cygwin or
with "bash on Windows".

List of dependencies (for version numbers refer to `lambdapi.opam`):
 - GNU make
 - [ocaml](https://ocaml.org/) (at least 4.05.0 and at most 4.07.1)
 - [dune](https://dune.build/)
 - [odoc](https://github.com/ocaml/odoc) (for documentation only)
 - [bindlib](https://github.com/rlepigre/ocaml-bindlib)
 - [earley](https://github.com/rlepigre/ocaml-earley)
 - [timed](https://github.com/rlepigre/ocaml-timed)
 - [menhir](http://gallium.inria.fr/~fpottier/menhir/)
 - [yojson](https://github.com/ocaml-community/yojson)
 - [cmdliner](https://erratique.ch/logiciel/cmdliner)
 - [why3](http://why3.lri.fr/)

**Note on OCaml versions:** more recent versions of OCaml will be supported
soon, once the new parsing technology that we are using has stabilized.

**Note on the use of Why3:** the command `why3 config --detect` must be run to
update the Why3 configuration when a new prover is installed (including on the
first installation of Why3).

Using Opam, a suitable OCaml environment can be setup as follows.
```bash
opam switch 4.07.1
eval `opam config env`
opam install dune odoc menhir yojson cmdliner bindlib.5.0.0 timed.1.0 earley.2.0.0 why3.1.3.1
why3 config --detect
```

To compile Lambdapi, just run the command `make` in the source directory.
This produces the `_build/install/default/bin/lambdapi` binary, which can
be run on files with the `.dk` or `.lp` extension (use the `--help` option
for more information).

```bash
make               # Build lambdapi.
make doc           # Build the documentation.
make install       # Install the program.
make install_vim   # Install vim support.
```

**Note:** you can run `lambdapi` without installing with `dune exec -- lambdapi`.

**Note on Emacs:** `make install` installs the `lambdapi-mode`, an Emacs major
mode for editing `lambdapi` files in `$(opam var share)/emacs/site-lisp`.
To load the `lambdapi-mode` automatically when editing `*.lp` files, add `(load
"lambdapi-site-file")` to your `~/.emacs.d/init.el` or `~/.emacs`.
If `lambdapi-mode` is not activated when editing a file ending in `.lp`, read
the installation section of the
[documentation](doc/sections/emacs.md#installation).

The following commands can be used for cleaning up the repository:
```bash
make clean     # Removes files generated by OCaml.
make distclean # Same as clean, but also removes library checking files.
make fullclean # Same as distclean, but also removes downloaded libraries.
```
