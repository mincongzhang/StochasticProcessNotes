```
https://python-fiddle.com/examples/matplotlib?checkpoint=1767058952
```

```
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm

# Parameters
T = 1.0
N = 1000
dt = T / N
t = np.linspace(0, T, N + 1)

# --- Brownian motion paths ---
num_paths = 30
paths = []

for _ in range(num_paths):
    dW = np.random.normal(0, np.sqrt(dt), size=N)
    W = np.concatenate(([0], np.cumsum(dW)))
    paths.append(W)

# --- Many paths for histogram ---
M = 10000
dW_all = np.random.normal(0, np.sqrt(dt), size=(M, N))
W_all = np.cumsum(dW_all, axis=1)
endpoints = W_all[:, -1]

# --- Combined figure with width ratios ---
fig, axes = plt.subplots(
    1, 2,
    figsize=(9, 6),
    sharey=True,
    gridspec_kw={'width_ratios': [4, 1]}
)

# ---------------------------------------------------------
# Left: Brownian paths with ±√t bounds (BOLD)
# ---------------------------------------------------------
ax = axes[0]

for W in paths:
    ax.plot(t, W, lw=2, alpha=0.5)   # bold paths

ax.plot(t, np.sqrt(t), 'r--', lw=3, label=r'$+\sqrt{t}$')   # bold envelope
ax.plot(t, -np.sqrt(t), 'b--', lw=3, label=r'$-\sqrt{t}$')  # bold envelope
ax.axhline(0, color='k', lw=3, label='0')                   # bold baseline

ax.set_title('Brownian Motion Paths with ±√t Bounds')
ax.set_xlabel('Time t')
ax.set_ylabel('Position B(t)')
ax.legend()
ax.grid(True)

# ---------------------------------------------------------
# Right: Horizontal histogram + normal PDF
# ---------------------------------------------------------
ax2 = axes[1]

ax2.hist(endpoints, bins=50, density=True, alpha=0.3,
         orientation='horizontal', label='Empirical B(1)')

y = np.linspace(-4, 4, 500)
pdf = norm.pdf(y, 0, np.sqrt(T))
ax2.plot(pdf, y, 'r', lw=2, alpha=0.7, label='Normal PDF N(0,1)')

ax2.set_xlim(0, 0.45)
ax2.set_xticks([0.2, 0.4])

ax2.set_title('Distribution of Brownian \n Endpoints at t=1')
ax2.set_xlabel('Density')
ax2.set_ylabel('Position B(1)')
ax2.legend()
ax2.grid(True)

plt.tight_layout()
plt.show()
```

<img width="900" height="600" alt="image" src="https://github.com/user-attachments/assets/ebe11ca5-3a1f-4605-ade8-b2c3c12fa0ee" />



```
import numpy as np
import matplotlib.pyplot as plt

# Parameters / reproducibility
np.random.seed(42)
N = 300
delta = 150  # larger horizontal distance for visibility

# Generate a 1D random walk (x = time/index, y = cumulative sum of steps)
x = np.arange(N)
steps = np.random.normal(loc=0.0, scale=1.0, size=N)
y = np.cumsum(steps)

# Pick two points whose x-index distance is <= epsilon
i = np.random.randint(0, N - delta)          # starting index
diff = np.random.randint(1, delta + 1)      # choose how far ahead (1..epsilon)
j = i + diff

# Compute slope A between the two chosen points
dx = x[j] - x[i]
dy = y[j] - y[i]
A = dy / dx

# Plot the random walk path
plt.figure(figsize=(12, 6))
plt.plot(x, y, color='tab:blue', lw=1, label='Random walk path')

# Highlight the two points and the connecting segment
plt.scatter([x[i], x[j]], [y[i], y[j]], color='red', zorder=5, s=70)
plt.plot([x[i], x[j]], [y[i], y[j]], color='orange', lw=3, zorder=4, label=f'Connecting segment (A={A:.3f})')

# Draw dashed right-angle markers for run & rise
plt.plot([x[i], x[j]], [y[i], y[i]], color='gray', ls='--', lw=1)
plt.plot([x[j], x[j]], [y[i], y[j]], color='gray', ls='--', lw=1)

# Label the two points as requested:
# first point (plotted first) -> B(t+epsilon), second -> B(t)
plt.annotate(r"$B(t)$", xy=(x[i], y[i]), xytext=(-10, 12),
             textcoords='offset points', ha='right', va='bottom', color='red',
             bbox=dict(facecolor='white', edgecolor='none', alpha=1))
plt.annotate(r"$B(t+\delta)$", xy=(x[j], y[j]), xytext=(8, -10),
             textcoords='offset points', ha='left', va='top', color='red',
             bbox=dict(facecolor='white', edgecolor='none', alpha=1))

# Label slope "A" near the midpoint, rotated to match slope
midx, midy = (x[i] + x[j]) / 2, (y[i] + y[j]) / 2
angle = np.degrees(np.arctan(A))
plt.text(midx, midy, "A \n\n", color='red', fontsize=14,
         bbox=dict(facecolor='white', edgecolor='none', alpha=0.9),
         rotation=angle, ha='center', va='center')

# Expand axis ranges for better view
x_margin = int(N * 0.10)
y_span = y.max() - y.min()
y_margin = y_span * 0.12
plt.xlim(x.min() - x_margin, x.max() + x_margin)
plt.ylim(y.min() - y_margin, y.max() + y_margin)

plt.xlabel('Index (x)')
plt.ylabel('Walk position (y)')
plt.title(f'Random walk with two points within delta={delta} (indices {i} and {j})')
plt.legend()
plt.grid(alpha=0.3)
plt.tight_layout()
plt.show()
```

<img width="1200" height="600" alt="image" src="https://github.com/user-attachments/assets/8af3344e-7d7d-4aee-b8a6-36faf6d9ea74" />



```
import numpy as np
import matplotlib.pyplot as plt

# -----------------------
# Parameters
# -----------------------
np.random.seed(2)

h = 1.0              # time window length
N = 1000             # steps in [t, t+h]
dt = h / N
s = np.linspace(0, h, N)

num_paths = 12
A = 2.5              # cone slope

# -----------------------
# Brownian increments on [t, t+h]
# -----------------------
paths = []

for _ in range(num_paths):
    dB = np.sqrt(dt) * np.random.randn(N)
    B = np.cumsum(dB)
    paths.append(B)

# -----------------------
# Cone lines ±A s
# -----------------------
upper_cone = A * s
lower_cone = -A * s

# -----------------------
# Plot
# -----------------------
plt.figure(figsize=(5, 5))

for B in paths:
    plt.plot(s, B, alpha=0.8)

# Red cone with 70% transparency
plt.plot(s, upper_cone, color='red', linewidth=3, alpha=0.7)
plt.plot(s, lower_cone, color='red', linewidth=3, alpha=0.7)

plt.axhline(0, color='blue', linewidth=2)

plt.title("Brownian Paths on [t, t+delta]")
plt.xlabel("delta = time since t")
plt.ylabel("B(t+delta) − B(t)")

plt.tight_layout()
plt.show()

```


<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/a331e132-a2c8-4b49-b3be-ad41ca1bc06c" />


```
import numpy as np
import matplotlib.pyplot as plt

# Parameters
T = 1.0
N = 20
dt = T / N
t = np.linspace(0, T, N + 1)

# Brownian motion
np.random.seed(23)
dB = np.random.normal(0, np.sqrt(dt), size=N)
B = np.concatenate(([0], np.cumsum(dB)))

# Smooth function
f = np.sin(2 * np.pi * t)
df = np.diff(f)

# Plot
fig, axes = plt.subplots(1, 2, figsize=(14, 5))

# ---------------- Brownian Motion ----------------
ax = axes[0]
ax.plot(t, B, color='blue')
ax.scatter(t, B, color='red')

for i in range(N):
    x0, x1 = t[i], t[i+1]
    y0, y1 = B[i], B[i+1]
    sq = (y1 - y0)**2

    # vertical increment line
    ax.plot([x0, x0], [y0, y1], 'k--', alpha=0.6)

    # rectangle showing squared increment
    ax.add_patch(plt.Rectangle((x0, min(y0, y1)), 
                               dt, sq, 
                               fill=False, edgecolor='black', linestyle=':'))

ax.set_title("Brownian Motion: Squared Increments")
ax.set_xlabel("t")
ax.set_ylabel("B(t)")
ax.grid(True)

# ---------------- Smooth Function ----------------
ax = axes[1]
ax.plot(t, f, color='blue')
ax.scatter(t, f, color='red')

for i in range(N):
    x0, x1 = t[i], t[i+1]
    y0, y1 = f[i], f[i+1]
    sq = (y1 - y0)**2

    ax.plot([x0, x0], [y0, y1], 'k--', alpha=0.6)

    ax.add_patch(plt.Rectangle((x0, min(y0, y1)), 
                               dt, sq, 
                               fill=False, edgecolor='black', linestyle=':'))

ax.set_title("Smooth Function: Squared Increments")
ax.set_xlabel("t")
ax.set_ylabel("f(t)")
ax.grid(True)

plt.tight_layout()
plt.show()
```

<img width="1400" height="500" alt="image" src="https://github.com/user-attachments/assets/cc6e94db-2bb5-4daf-80cb-c06d0eae54b6" />


```
import numpy as np
import matplotlib.pyplot as plt

T = 1.0
num_partitions = np.logspace(1, 4, 20, dtype=int)  # from 10 to 10,000 intervals

QV_brownian = []
QV_smooth = []

np.random.seed(42)

for N in num_partitions:
    dt = T / N
    t = np.linspace(0, T, N+1)

    # Brownian motion increments
    dB = np.random.normal(0, np.sqrt(dt), size=N)
    QV_brownian.append(np.sum(dB**2))

    # Smooth function f(t) = sin(2πt)
    f = np.sin(2*np.pi*t)
    df = np.diff(f)
    QV_smooth.append(np.sum(df**2))

# Plot
plt.figure(figsize=(10,6))
plt.plot(num_partitions, QV_brownian, 'o-', label='Brownian motion')
plt.plot(num_partitions, QV_smooth, 'o-', label='Smooth function')
plt.axhline(1.0, color='gray', linestyle='--', label='T = 1')

plt.xscale('log')
plt.xlabel("Number of intervals (log scale)")
plt.ylabel("Quadratic variation")
plt.title("Quadratic Variation vs Partition Size")
plt.legend()
plt.grid(True)
plt.show()
```

<img width="1000" height="600" alt="image" src="https://github.com/user-attachments/assets/95b4178f-1a79-4a1e-a5b7-296346171889" />

```
import numpy as np
import matplotlib.pyplot as plt

# parameters
mu = 1.0
epsilon = 0.2
T = 1000
dt = 0.1

# time grid
t = np.arange(0, T, dt)

# Brownian motion
dB = np.sqrt(dt) * np.random.randn(len(t))
B = np.cumsum(dB)

# Brownian motion with drift
X = B + mu * t

# bounding lines
upper = (mu + epsilon) * t
lower = (mu - epsilon) * t

# plot
plt.figure(figsize=(10, 6))
plt.plot(t, X, label="X(t) = B(t) + μt", linewidth=1)
plt.plot(t, upper, 'r--', label="y=(μ + ε)t")
plt.plot(t, lower, 'r--', label="y=(μ - ε)t")

plt.xlabel("t")
plt.ylabel("value")
plt.title("Brownian Motion with Drift Eventually Stays Between Two Lines")
plt.legend()
plt.grid(True)
plt.show()
```

<img width="1000" height="600" alt="image" src="https://github.com/user-attachments/assets/0ee84b53-b65a-4db6-8d08-5beb06e9d0ea" />
