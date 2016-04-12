usage: gochecker [-h] [-v] [-l] [-r] [targets [targets ...]]

A frontend for `go test` and gocheck.

positional arguments:
  targets        Directory, package, suite and/or test to run. By default, all
                 tests will be run recursively from the current directory.

optional arguments:
  -h, --help     show this help message and exit
  -v, --verbose  Verbose test output (use twice for extra effect)
  -l, --logs     Show log output when tests fail
  -r, --race     Enable race detector

Some examples of how gochecker converts its args to `go test` command lines:

  gochecker                         : go test ./...
  gochecker -v ...                  : go test -v ./... -gocheck.v
  gochecker -v foo                  : go test -v ./foo -gocheck.v
  gochecker -v foo/...              : go test -v ./foo/... -gocheck.v
  gochecker -vv foo                 : go test -v ./foo -gocheck.vv
  gochecker foo:SomeSuite           : go test ./foo -gocheck.f SomeSuite
  gochecker foo:SomeSuite.TestThing : go test ./foo -gocheck.f SomeSuite.TestThing
  gochecker --race foo              : go test -r ./foo

Testing across multiple packages is also supported. For example:

  gochecker foo bar:SomeSuite some/other/package

All output is recorded to a gochecker-*.out files. The last 3 output
files are kept.

By default, logger output to the console is suppressed, but will be
available in the output files. To see logger output at the console
pass --logs or -l.
