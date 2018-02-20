# numir-char-rnn

rewrite [tiny numpy RNN](https://gist.github.com/karpathy/d4dee566867f8291f086) in D and numir.

## how to use

``` console
$ wget https://raw.githubusercontent.com/karpathy/char-rnn/master/data/tinyshakespeare/input.txt

$ export OMP_NUM_THREADS=1

$ time dub run -b=release-nobounds --compiler=ldc2
...
iter 9900, loss: 54.215532, iter/sec: 1190.476190
dub run -b=release-nobounds --compiler=ldc2  8.74s user 0.26s system 98% cpu 9.164 total

$ time dub run -b=release-nobounds --compiler=dmd
...
iter 9900, loss: 56.192083, iter/sec: 751.879699
dub run -b=release-nobounds --compiler=dmd  13.65s user 0.10s system 98% cpu 13.998 total

$ time python rnn.py
...
iter 9900, loss: 56.515613, iter/sec 337.730925
python rnn.py  29.94s user 0.06s system 99% cpu 30.050 total
```

## results

my environment 
- anaconda=4.3.30
- numpy=1.13.3
- numir=0.1.0 (see dub.selections.json)
- BLAS/Lapack=IntelMKL in anaconda
- CPU=Intel(R) Xeon(R) CPU E5-2695 v3 @ 2.30GHz

| lib                 | `OMP_NUM_THREADS` | 10000 iter time (sec) | 10000 iter loss |
| :--                 | :--               |                   --: |             --: |
| numpy               | unset             |                109.87 |           57.21 |
| numir (dmd 2.078.3) | unset             |                 57.43 |           52.98 |
| numir (ldc2 1.7.0)  | unset             |                 40.64 |           56.14 |
| numpy               | 1                 |                 29.94 |           56.51 |
| numir (dmd 2.078.3) | 1                 |                 13.65 |           56.19 |
| numir (ldc2 1.7.0)  | 1                 |              **8.41** |           54.93 |

numir is about 3.5 times faster than numpy


# examples

after 1000000 iter (13 min), the sampled chars become

```
deremer not o', spear                                                                                                       
So; these were through kis.                                                                                                 
                                                                                                                            
HENRY PERCY:                                                                                                                
Him!                                                                                                                        
Now'd man is a many bone chait.                                                                                             
Th.                                                                                                                         
                                                                                                                            
THIN:                                                                                                                       
Nor air true evern dey'd truity I coming warn you hands                                                                     
Finched Tybsh soultan the is wit 
-----
iter 999900, loss: 43.986925, iter/sec: 1204.819277           
dub run -b=release-nobounds --compiler=ldc2  829.59s user 1.04s system 99% cpu 13:52.50 total
```

