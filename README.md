<!--

@license Apache-2.0

Copyright (c) 2026 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# fillRange

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Fill an input [ndarray][@stdlib/ndarray/ctor] with a specified value along an [ndarray][@stdlib/ndarray/ctor] dimension.

<section class="installation">

## Installation

```bash
npm install @stdlib/blas-ext-fill-range
```

Alternatively,

-   To load the package in a website via a `script` tag without installation and bundlers, use the [ES Module][es-module] available on the [`esm`][esm-url] branch (see [README][esm-readme]).
-   If you are using Deno, visit the [`deno`][deno-url] branch (see [README][deno-readme] for usage intructions).
-   For use in Observable, or in browser/node environments, use the [Universal Module Definition (UMD)][umd] build available on the [`umd`][umd-url] branch (see [README][umd-readme]).

The [branches.md][branches-url] file summarizes the available branches and displays a diagram illustrating their relationships.

To view installation and usage instructions specific to each branch build, be sure to explicitly navigate to the respective README files on each branch, as linked to above.

</section>

<section class="usage">

## Usage

```javascript
var fillRange = require( '@stdlib/blas-ext-fill-range' );
```

#### fillRange( x, value\[, start\[, end]]\[, options] )

Fills an input [ndarray][@stdlib/ndarray/ctor] with a specified value along an [ndarray][@stdlib/ndarray/ctor] dimension.

```javascript
var array = require( '@stdlib/ndarray-array' );

// Create an input ndarray:
var x = array( [ 1.0, 2.0, 3.0, 4.0, 5.0, 6.0 ] );
// returns <ndarray>[ 1.0, 2.0, 3.0, 4.0, 5.0, 6.0 ]

// Perform operation:
var y = fillRange( x, 10.0, 1, 4 );
// returns <ndarray>[ 1.0, 10.0, 10.0, 10.0, 5.0, 6.0 ]

var bool = ( x === y );
// returns true
```

The function has the following parameters:

-   **x**: input [ndarray][@stdlib/ndarray/ctor].
-   **value**: fill value. May be either a scalar value or an [ndarray][@stdlib/ndarray/ctor]. Must be able to safely cast to the input [ndarray][@stdlib/ndarray/ctor] [data type][@stdlib/ndarray/dtypes]. Values having floating-point [data types][@stdlib/ndarray/dtypes] (both real and complex) are allowed to downcast to a lower precision [data type][@stdlib/ndarray/dtypes] of the same kind (e.g., a scalar double-precision floating-point number can be used to fill a `'float32'` input [ndarray][@stdlib/ndarray/ctor]). If provided an [ndarray][@stdlib/ndarray/ctor], the value must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the complement of the shape defined by `options.dim`. For example, given the input shape `[2, 3, 4]` and `options.dim=0`, an [ndarray][@stdlib/ndarray/ctor] fill value must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the shape `[3, 4]`.
-   **start**: starting index (inclusive) (_optional_). May be either an integer or an [ndarray][@stdlib/ndarray/ctor] having an integer index or "generic" [data type][@stdlib/ndarray/dtypes] and following the same broadcasting semantics as an [ndarray][@stdlib/ndarray/ctor] `value` argument. Default: `0`.
-   **end**: ending index (exclusive) (_optional_). May be either an integer or an [ndarray][@stdlib/ndarray/ctor] having an integer index or "generic" [data type][@stdlib/ndarray/dtypes] and following the same broadcasting semantics as an [ndarray][@stdlib/ndarray/ctor] `value` argument. By default, the ending index is `N`, where `N` is the number of elements along the dimension specified by `options.dim`.
-   **options**: function options (_optional_).

The function accepts the following options:

-   **dim**: dimension over which to perform operation. If provided a negative integer, the dimension along which to perform the operation is determined by counting backward from the last dimension (where `-1` refers to the last dimension). Default: `-1`.

When a `start` and/or `end` index is negative, the respective index is determined relative to the last indexed element, with out-of-bounds indices clamped to index bounds.

```javascript
var array = require( '@stdlib/ndarray-array' );

var x = array( [ 1.0, 2.0, 3.0, 4.0, 5.0, 6.0 ] );

var y = fillRange( x, 10.0, -2 );
// returns <ndarray>[ 1.0, 2.0, 3.0, 4.0, 10.0, 10.0 ]
```

By default, the function performs the operation over elements along the last dimension. To perform the operation over a different dimension, provide a `dim` option.

```javascript
var array = require( '@stdlib/ndarray-array' );

var x = array( [ [ 1.0, 2.0, 3.0, 4.0 ], [ 5.0, 6.0, 7.0, 8.0 ] ] );

var y = fillRange( x, array( [ 9.0, 10.0, 11.0, 12.0 ] ), {
    'dim': 0
});
// returns <ndarray>[ [ 9.0, 10.0, 11.0, 12.0 ], [ 9.0, 10.0, 11.0, 12.0 ] ]
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   The input [ndarray][@stdlib/ndarray/ctor] is filled **in-place** (i.e., the input [ndarray][@stdlib/ndarray/ctor] is **mutated**).

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```javascript
var discreteUniform = require( '@stdlib/random-discrete-uniform' );
var ndarray2array = require( '@stdlib/ndarray-to-array' );
var fillRange = require( '@stdlib/blas-ext-fill-range' );

// Generate an ndarray of random numbers:
var x = discreteUniform( [ 5, 5 ], 0, 20, {
    'dtype': 'generic'
});
console.log( ndarray2array( x ) );

// Perform operation:
fillRange( x, 0, 1, 4, {
    'dim': 0
});

// Print the results:
console.log( ndarray2array( x ) );
```

</section>

<!-- /.examples -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/blas-ext-fill-range.svg
[npm-url]: https://npmjs.org/package/@stdlib/blas-ext-fill-range

[test-image]: https://github.com/stdlib-js/blas-ext-fill-range/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/blas-ext-fill-range/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/blas-ext-fill-range/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/blas-ext-fill-range?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/blas-ext-fill-range.svg
[dependencies-url]: https://david-dm.org/stdlib-js/blas-ext-fill-range/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/blas-ext-fill-range/tree/deno
[deno-readme]: https://github.com/stdlib-js/blas-ext-fill-range/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/blas-ext-fill-range/tree/umd
[umd-readme]: https://github.com/stdlib-js/blas-ext-fill-range/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/blas-ext-fill-range/tree/esm
[esm-readme]: https://github.com/stdlib-js/blas-ext-fill-range/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/blas-ext-fill-range/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/blas-ext-fill-range/main/LICENSE

[@stdlib/ndarray/ctor]: https://github.com/stdlib-js/ndarray-ctor

[@stdlib/ndarray/dtypes]: https://github.com/stdlib-js/ndarray-dtypes

[@stdlib/ndarray/base/broadcast-shapes]: https://github.com/stdlib-js/ndarray-base-broadcast-shapes

</section>

<!-- /.links -->
