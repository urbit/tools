# click

[click](https://github.com/urbit/vere/blob/develop/bin/click) is a `bash` thin
client which auto-formats `-eval` and `-khan-eval` thread calls via `%fyrd`
requests to `conn.c` and coordinates chaining together the appropriate commands
to execute those requests on a running ship.

Using click, a call like:
```
echo $'[0 %fyrd %base %khan-eval %noun %ted-eval \'=/  m  (strand ,vase)  ;<  ~  bind:m  (poke [~zod %hood] %helm-hi !>(\\\'\\\'))  (pure:m !>(\\\'success\\\'))\']' |
/path/to/urbit eval -jn |
nc -U -W 1 /path/to/zod/.urb/conn.sock |
/path/to/urbit eval -cn
```
instead looks like:
```
/path/to/click -k /path/to/zod $'=/  m  (strand ,vase)  ;<  ~  bind:m  (poke [~zod %hood] %helm-hi !>(\\\'\\\'))  (pure:m !>(\\\'success\\\'))'
```
or even more conveniently:
```
/path/to/click -k -i threads/poke.hoon /path/to/zod
```

## Dependencies

click requires the OpenBSD version of `netcat` (a.k.a. `netcat-openbsd`) and not
the GNU version (a.k.a. `netcat-traditional`).

## Usage

```
Usage:
    click [options] <path-to-pier> <hoon> [<dependencies> ...]
    click [options] -i <path-to-file> <path-to-pier> [<dependencies> ...]
    click [-o|-p] -e -i <path-to-file> <path-to-pier>

    Thin client for interacting with running Urbit ship via conn.c

    options:
        -e                  Execute jammed Hoon
        -h                  Show usage info
        -i <path-to-file>   Read input from file
        -j                  Jam only
        -k                  Execute command using "khan-eval" thread
        -o <path-to-file>   Output to file
        -p                  Filter failure stack traces from result and pretty-print them to stderr
        -x                  Jam to hex
```
