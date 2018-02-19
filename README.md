# numir-char-rnn

rewrite [tiny numpy RNN](https://gist.github.com/karpathy/d4dee566867f8291f086) in D and numir.

## how to use

``` console
$ wget https://raw.githubusercontent.com/karpathy/char-rnn/master/data/tinyshakespeare/input.txt
$ dub run -b=release-release-nobounds
$ python rnn.py
```

in my environment (anaconda=4.3.30, numpy=1.13.3, numir=0.1.0, BLAS/Lapack=IntelMKL)

| lib   |   iter/sec | loss at 10000 iter |
| :--   |        --: |                --: |
| numpy | 548.787952 |              52.28 |
| numir | 735.294118 |              53.31 |

