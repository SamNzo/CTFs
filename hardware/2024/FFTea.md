# FFTea
## Hardware
### Intro

```python
import numpy as np

# get data from file
data = np.fromfile("fftea", dtype=np.complex64)

# fourier transform
result = np.array(np.fft.fft(data, n=64), dtype=np.complex64)

# get real values and cast to int
result = [int(x.real) for x in result]

# ascii to str
flag = "".join(chr(num) for num in result)

print(flag)
```

**FCSC{5b969113668d7fc28fe1a7d07183eea4de5458dd1027d6f29c24350a10}**
