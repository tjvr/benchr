## benchr

Node.js benchmark runner, modelled after [`Mocha`](http://mochajs.org/) and [`bencha`](https://www.npmjs.com/package/bencha), based on [Benchmark.js](http://benchmarkjs.com/).

Work in progress!

### Installation

```
$ npm i benchr [-g]
```

### Usage

Run the `benchr` script and provide it with files containing benchmarks:

```
$ benchr benchmarks/**/*.js
```

### Options

```
$ benchr -r
benchr – benchmark runner

Usage:
  benchr [options] <file>...

Options:
  -h --help           Show this screen
  -v --version        Show version
  -d --delay=<s>      Delay between test cycles, in seconds       [default: 0]
  -M --min-time=<s>   Minimum run time per test cycle, in seconds [default: 0]
  -m --max-time=<s>   Maximum run time per test cycle, in seconds [default: 5]
```

### Suites + benchmarks

A benchmark file declares one or more suites, each with one or more benchmarks to run.

For example:

```javascript
suite('Finding a substring', function() {

  benchmark('RegExp#test', function() {
    /o/.test('Hello World!');
  });

  benchmark('String#indexOf', function() {
    'Hello World!'.indexOf('o') > -1;
  });

  benchmark('String#match', function() {
    !!'Hello World!'.match(/o/);
  });

});

// A contrived async example. Just like with Mocha, when a benchmark accepts
// an argument it is assumed the benchmark should be run async.
suite('Finding a substring, async style', function() {

  benchmark('RegExp#test', function(done) {
    /o/.test('Hello World!');
    done();
  });

  benchmark('String#indexOf', function(done) {
    'Hello World!'.indexOf('o') > -1;
    done();
  });

  benchmark('String#match', function(done) {
    !!'Hello World!'.match(/o/);
    done();
  });

});
```

(taken from the example on the [Benchmark.js](http://benchmarkjs.com/) website).

### TODO

- [ ] Before/after hooks
- [x] ~~~Benchmark/suite options (minTime, maxTime, ...)~~~
- [ ] Separate reporters (very hardcoded now)
- [x] Handle multiple "fastest" benchmarks better
- [ ] Promise support (just like Mocha) (may be difficult to implement)
