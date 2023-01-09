# rly

`rly` is a concurrent task runner and, in its current form, essentially a clone of [concurrently](https://github.com/open-cli-tools/concurrently). For example:

```
$ rly --names "server,client" \
    "nc -l 1234" \
    "echo 'message from client' | nc localhost 1234"
[server] message from client
[server] nc -l 1234 exited with exit status: 0
[client] echo 'foo' | nc localhost 1234 exited with exit status: 0
```

## Usage (in progress)

```
Usage: rly [OPTIONS] [COMMANDS]...

Arguments:
  [COMMANDS]...


Options:
  -n, --names <NAMES>
          List of custom names to be used in prefix template.

          Example names: "main,browser,server"

      --name-separator <NAME_SEPARATOR>
          The character to split <names> on.

          Example usage: -n "styles|scripts|server" --name-separator
          "|"

          [default: ,]

  -r, --raw
          Output only raw output of processes, disables prettifying
          and concurrently coloring

      --no-color
          Disables colors from logging

      --hide <HIDE>
          Comma-separated list of processes for which to hide the
          output. The processes can be identified by their name or
          index

  -g, --group
          Order the output as if the commands were run sequentially

      --timings
          Show timing information for all processes

  -P, --passthrough-arguments
          Passthrough additional arguments to commands (accessible via
          placeholders) instead of treating them as commands

  -p, --prefix <PREFIX>
          Prefix used in logging for each process. Possible values:
          index, pid, time, command, name, none, or a template.
          Example template: "{time}-{pid}"

          [default: [{name}]]

  -c, --prefix-colors <PREFIX_COLORS>
          Comma-separated list of chalk colors to use on prefixes. If
          there are more commands than colors, the last color will be
          repeated.

          - Available modifiers: reset, bold, dim, italic, underline,
          inverse, hidden, strikethrough

          - Available colors: black, red, green, yellow, blue,
          magenta, cyan, white, gray, any hex values for colors (e.g.
          #23de43) or auto for an automatically picked color

          - Available background colors: bgBlack, bgRed, bgGreen,
          bgYellow, bgBlue, bgMagenta, bgCyan, bgWhite

          See https://www.npmjs.com/package/chalk for more
          information.

          [default: reset]

  -l, --prefix-length <PREFIX_LENGTH>
          Limit how many characters of the command is displayed in
          prefix. The option can be used to shorten the prefix when it
          is set to "command"

          [default: 10]

  -t, --timestamp-format <TIMESTAMP_FORMAT>
          Specify the timestamp in chrono::format syntax

          [default: "%Y-%m-%d %H:%M:%S.%3f"]

  -k, --kill-others
          Kill other processes if one exits or dies

      --kill-others-on-fail
          Kill other processes if one exits with non zero status code

      --restart-tries <RESTART_TRIES>
          How many times a process that died should restart. Negative
          numbers will make the process restart forever

          [default: 0]

      --restart-after <RESTART_AFTER>
          Delay time to respawn the process, in milliseconds

          [default: 0]

  -h, --help
          Print help information (use `-h` for a summary)

  -V, --version
          Print version information
```

## Why?

I like the UX of `concurrently`, but dislike having to install NodeJS / npm to use it. My goal is to make `rly` accessible via Homebrew (and potentially other package managers), so that installation only requires downloading a single binary. 


## Progress implementing `concurrently` features

- [x] commands can be supplied
- [x] `--names` can be passed
- [x] `--name-separator`
- [ ] `--raw`
- [x] `--no-color`
- [ ] `--hide`
- [ ] `--timings`
- [ ] `--passthrough-arguments`
- [x] `--prefix`
  - [x] index
  - [x] pid
  - [x] time
  - [x] command
  - [x] name
- [x] `--prefix-colors`
- [x] `--prefix-length`
- [x] `--timestamp-format`
- [ ] `--kill-others`
- [ ] `--kill-others-on-fail`
- [x] `--restart-tries`
- [x] `--restart-after`


# License

See `LICENSE` file.