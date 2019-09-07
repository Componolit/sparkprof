# About

This is a wrapper around the [SPARK](https://www.adacore.com/about-spark) proof
tool `gnatprove` to report excessive proof times as warnings/errors to help
optimizing the overall proof time.

# Usage

The `sparkprof` wrapper must be be called instead of `gnatprove`. The
`gnatprove` program must be in your PATH. When using the wrapper, two new
options are available: `--steps-warn=` and `steps-error=`. The former sets the
number of prove steps that trigger a warning when exceeded and latter the
number of proof steps that trigger an error when exceeded.

The wrapper is used as follows:

```sh
$ sparkprof -P project --steps=500 --steps-warn=20 --steps-error=200
...
Phase 1 of 2: generation of Global contracts ...
Phase 2 of 2: flow analysis and proof ...
extracts.adb:33:25: error: too many steps: assertion proved (CVC4: 1 VC in max (9.1) seconds and 355 steps), in instantiation at tests.adb:46, in instantiation at tests.adb:62
extracts.adb:62:97: warning: too many steps: overflow check proved (CVC4: 1 VC in max (9.3) seconds and 192 steps), in instantiation at tests.adb:46, in instantiation at tests.adb:59
...
```

# Limitations

Experimental and largely untested! Info message about proved VCs are filtered
out and not displayed when using the wrapper. Specifying seconds instead of
steps is imaginable, but not currently implemented.
