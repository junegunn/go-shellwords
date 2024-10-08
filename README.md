# go-shellwords

[![codecov](https://codecov.io/gh/mattn/go-shellwords/branch/master/graph/badge.svg)](https://codecov.io/gh/mattn/go-shellwords)
[![Build Status](https://travis-ci.org/mattn/go-shellwords.svg?branch=master)](https://travis-ci.org/mattn/go-shellwords)
[![PkgGoDev](https://pkg.go.dev/badge/github.com/mattn/go-shellwords)](https://pkg.go.dev/github.com/mattn/go-shellwords)
[![ci](https://github.com/mattn/go-shellwords/ci/badge.svg)](https://github.com/mattn/go-shellwords/actions)

Parse line as shell words.

## Usage

```go
args, err := shellwords.Parse("./foo --bar=baz")
// args should be ["./foo", "--bar=baz"]
```

```go
envs, args, err := shellwords.ParseWithEnvs("FOO=foo BAR=baz ./foo --bar=baz")
// envs should be ["FOO=foo", "BAR=baz"]
// args should be ["./foo", "--bar=baz"]
```

```go
os.Setenv("FOO", "bar")
p := shellwords.NewParser()
p.ParseEnv = true
args, err := p.Parse("./foo $FOO")
// args should be ["./foo", "bar"]
```

```go
p := shellwords.NewParser()
p.ParseBacktick = true
args, err := p.Parse("./foo `echo $SHELL`")
// args should be ["./foo", "/bin/bash"]
```

```go
shellwords.ParseBacktick = true
p := shellwords.NewParser()
args, err := p.Parse("./foo `echo $SHELL`")
// args should be ["./foo", "/bin/bash"]
```

```go
p := shellwords.NewParser()
p.ParseComment = true
args, err := p.Parse("./foo # comment")
// args should be ["./foo"]
```

# Thanks

This is based on cpan module [Parse::CommandLine](https://metacpan.org/pod/Parse::CommandLine).

# License

under the MIT License: http://mattn.mit-license.org/2017

# Author

Yasuhiro Matsumoto (a.k.a mattn)
