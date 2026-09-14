# Random directions become orthogonal

A compact, reproducible demonstration of a high-dimensional geometry effect: two independent random directions are increasingly likely to form an angle close to 90° as the number of dimensions grows.

The program samples pairs of vectors from a standard normal distribution, normalizes them to the unit sphere, and measures the angle between every pair. The animation shows both the changing angle distribution and the shrinking average distance from 90°.

## Run it

### System dependency

The animation opens a Tk window, so install Tk through your operating system first. It is intentionally a system dependency rather than a large Python GUI package:

```bash
# Arch Linux
sudo pacman -S tk

# Debian/Ubuntu
sudo apt install python3-tk
```

Run the program from a graphical desktop session. For an SSH session, use X11 forwarding (for example, `ssh -X host`).

```bash
git clone https://github.com/thestubbornbat/random-directions-orthogonality.git
cd random-directions-orthogonality
python -m pip install -r requirements.txt
python orthogonality_animation.py
```

Running the script opens a small Matplotlib window. It cycles from 2 to 1,000 dimensions: the histogram narrows around the dashed 90° line, while the right-hand plot records the concentration.

## Options

```bash
python orthogonality_animation.py --samples 10000 --interval 600
```

Use `--seed -1` for a new random draw on every run.

## Use from Python

```python
from orthogonality_animation import animate_orthogonality

animate_orthogonality(dimensions=[2, 10, 100, 1_000], samples=10_000)
```

## Why this happens

For two independent random unit vectors $a, b \in \mathbb{R}^n$,

$$
\cos(\theta) = a \cdot b, \qquad \mathbb{E}[a \cdot b] = 0, \qquad \mathrm{Var}(a \cdot b) = \frac{1}{n}.
$$

The dot product therefore concentrates near zero as $n$ grows. Since $\cos(90^\circ)=0$, the angle concentrates near 90°.

## License

[MIT](LICENSE)
