# Gradualizer plugin for rebar3

To run Gradualizer from rebar3, add it as a plugin in your `rebar.config`:
```Erlang
{plugins, [
  {gradualizer, {git, "git@github.com:josefs/Gradualizer.git", {branch, "master"}}}
]}.
```

# Analyzing erl files or beam files

Gradualizer can process both `*.erl` files and `*.beam` files.

By default, `rebar3 gradualizer` processes `*.erl` files from source directories.
In this default mode gradualizer tries its best to get include directories, header files
and compiler options right. However, in case of complex setup gradualizer may miss something.

`rebar3 gradualizer --use_beams` uses `*.beam` files from `ebin` directories as input
(beam files should be produced with debug info to be analyzable).

`--use_beams` may be a more robust choice if there are problems with analyzing `*.erl` files.

# Options (`gradualizer_opts`)

Gradualizer checks every source file in your app(s), unless configured not to.
Configuration is read from `gradualizer_opts` in `rebar.config` which
should be a `proplists:proplist()`.
The following options are supported:

## include

type: `[filelib Wildcard]`

Files to type check - Gradualizer includes every `.erl` file in the source directory if undefined

## exclude

type: `[filelib Wildcard]`

Files to not type check. Subtracts the list of included files

## stop_on_first_error

type: `boolean()`

if 'true' stop type checking at the first error, if 'false' continue checking all functions in the given file and all files in the given directory
