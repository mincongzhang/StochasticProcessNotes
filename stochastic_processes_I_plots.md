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

# --- Random walk (discrete-time) paths ---
num_paths = 50
walks = []

for _ in range(num_paths):
    dW = np.random.normal(0, np.sqrt(dt), size=N)
    W = np.concatenate(([0], np.cumsum(dW)))
    walks.append(W)

# --- Many walks for histogram of endpoints ---
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

# Left: Random walk paths (no 0 baseline)
ax = axes[0]

for i, W in enumerate(walks):
    label = 'Random walk paths' if i == 0 else None
    ax.plot(t, W, lw=2, alpha=0.5, label=label)

ax.set_title('Random Walk Paths')
ax.set_xlabel('Time t')
ax.set_ylabel('Position')
ax.legend()
ax.grid(True)

# Right: Horizontal histogram + normal PDF
ax2 = axes[1]

ax2.hist(endpoints, bins=50, density=True, alpha=0.3,
         orientation='horizontal', label='Empirical S(1)')

y = np.linspace(-4, 4, 500)
pdf = norm.pdf(y, 0, np.sqrt(T))
ax2.plot(pdf, y, 'r', lw=2, alpha=0.7, label='Normal PDF N(0,1)')

ax2.set_xlim(0, 0.45)
ax2.set_xticks([0.2, 0.4])

ax2.set_title('Distribution of Random Walk \n Endpoints at t=1')
ax2.set_xlabel('Density')
ax2.set_ylabel('Position S(1)')
ax2.legend()
ax2.grid(True)

plt.tight_layout()
plt.show()
```

<img width="900" height="600" alt="image" src="https://github.com/user-attachments/assets/f3c0e68b-24e6-40a0-9204-6e369d99b627" />
