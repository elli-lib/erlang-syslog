# Erlang driver for syslog

[![Build Status][Travis badge]][Travis link]

[Travis badge]: https://travis-ci.org/yurrriq/erlang-syslog.svg?branch=master
[Travis link]: https://travis-ci.org/yurrriq/erlang-syslog

This is an Erlang port driver for interacting with syslog.

## Building

```fish
rebar3 compile
```


## Usage

You should have a look at `syslog.h`.

In another shell:

```fish
tail -f /var/log/syslog
```

Or, for mac users:

```fish
tail -f /var/log/system.log
```

In an Erlang shell:

```erlang
> syslog:start().
> {ok,Log} = syslog:open("Beuha", [cons, perror, pid], local0).
> syslog:log(Log, err, "Damned").
> syslog:log(Log, info, "process count: ~w", [length(processes())]).
```


## API

```erlang
-type openlog_opt() :: pid | cons | odelay | ndelay | perror | pos_integer().

-type facility() :: kern    | user       | mail     | daemon
                  | auth    | syslog     | lpr      | news
                  | uucp    | cron       | authpriv | ftp
                  | netinfo | remoteauth | install  | ras
                  | local0  | local1     | local2   | local3
                  | local4  | local5     | local6   | local7
                  | non_neg_integer().

-type priority() :: emerg   | alert  | crit | err
                  | warning | notice | info | debug
                  | non_neg_integer().

-spec open(Ident, LogOpt, Facility) -> {ok, Log} |  {error, any()} when
      Ident    :: string(),
      LogOpt   :: openlog_opt() | [openlog_opt()],
      Facility :: facility(),
      Log      :: port().

-spec log(Log :: port(), Priority :: priority(), Message :: iolist()) -> ok.

-spec log(Log, Priority, Format, Data) -> ok when
      Log      :: port(),
      Priority :: priority(),
      Format   :: io:format(),
      Data     :: [term()].

-spec close(Log :: port()) -> ok.
```

## BUGS

 * None known
