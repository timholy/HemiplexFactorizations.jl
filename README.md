# HemiplexFactorizations

[![CI](https://github.com/timholy/HemiplexFactorizations.jl/actions/workflows/CI.yml/badge.svg)](https://github.com/timholy/HemiplexFactorizations.jl/actions/workflows/CI.yml)
[![codecov](https://codecov.io/gh/timholy/HemiplexFactorizations.jl/graph/badge.svg?token=ldfY1pgacu)](https://codecov.io/gh/timholy/HemiplexFactorizations.jl)

# Introduction

Cholesky factorizations over the hemiplex numbers can be computed for
arbitrary symmetric matrices, including indefinite and singular
matrices.  For singular matrices, the behavior is reminiscent of the
singular value decomposition, but the performance is much better.
The method is described in [Edelman & Holy,
arXiv:2607.21383](https://arxiv.org/abs/2607.21383); the number system
itself lives in
[HemiplexNumbers.jl](https://github.com/timholy/HemiplexNumbers.jl).

# Usage

After creating a symmetric matrix `A`, compute its Cholesky
factorization over the hemiplex numbers like this:

```jl
F = cholfact(PureHemi, A)
```
Then you can use `F` to solve equations, e.g.,
```jl
x = F \ b
```
If `A` has zero pivots, you will need to use `x = nullsolver(F) \ b` instead.

If `A` is singular, this should be the least-squares solution.

## Supported operations

You can compute `F*F'` or say `rank(F)`.  You can also convert `F`
into matrix form with `convert(Matrix, F)`.

## Options

```jl
F = cholfact(PureHemi, A, δ; blocksize=default)
```
where:

- `δ` is the tolerance on the diagonal values of `A` during factorization; any with magnitudes smaller than `δ` will be treated as if they are 0.
- `blocksize` controls the performance of the factorization algorithm.

# Citation

If you use this package in published work, please cite:

> A. Edelman and T. E. Holy, "Jordan algebras, hemiplex numbers, and the
> Cholesky decomposition of arbitrary symmetric matrices," arXiv:2607.21383
> (2026). https://doi.org/10.48550/arXiv.2607.21383

```bibtex
@article{EdelmanHoly2026,
  author  = {Edelman, Alan and Holy, Timothy E.},
  title   = {Jordan algebras, hemiplex numbers, and the {Cholesky}
             decomposition of arbitrary symmetric matrices},
  journal = {arXiv},
  year    = {2026},
  doi     = {10.48550/arXiv.2607.21383},
  url     = {https://arxiv.org/abs/2607.21383},
}
```

Machine-readable metadata is in [`CITATION.cff`](CITATION.cff).
