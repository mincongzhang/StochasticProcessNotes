```
https://python-fiddle.com/examples/matplotlib?checkpoint=1767058952
```

```
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(2)

# Use n_steps=6 so positions has 7 points (0..6)
n_steps = 6
increments = np.random.normal(scale=1.0, size=n_steps)
positions = np.concatenate(([0.0], np.cumsum(increments)))  # length 7
times = np.arange(len(positions))

# pick t so t+1 is valid (0 <= t < n_steps)
t = 3
t1 = t + 1

plt.figure(figsize=(8, 3.5))
plt.plot(times, positions, '-o', markersize=8, alpha=0.8, label='Random walk (first 7 steps)')

# Highlight t and t+1 (no special start/end markers)
plt.scatter(t,  positions[t],  color='red',   s=150, zorder=5, label='t')
plt.scatter(t1, positions[t1], color='green', s=150, zorder=5, label='t+1')

# Arrow from t to t+1 and text labels
plt.annotate('', xy=(t1, positions[t1]), xytext=(t, positions[t]),
             arrowprops=dict(arrowstyle='->', color='orange', lw=2), zorder=6)
plt.text(t,  positions[t],  '  t\n',  color='red',   fontsize=12, va='bottom')
plt.text(t1, positions[t1], '  t+1\n', color='green', fontsize=12, va='bottom')

plt.xticks(times)
plt.xlabel(f'Time (step={n_steps})')
plt.ylabel('Position')
plt.title('Random Walk')
plt.grid(alpha=0.3)
plt.tight_layout()
plt.show()
```

<img width="800" height="350" alt="image" src="https://github.com/user-attachments/assets/4b87d001-b300-4359-aa07-6c71bb381605" />


```
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(2)

# Use n_steps=6 so positions has 7 points (0..6)
n_steps = 600
increments = np.random.normal(scale=1.0, size=n_steps)
positions = np.concatenate(([0.0], np.cumsum(increments)))  # length 7
times = np.arange(len(positions))

# pick t so t+1 is valid (0 <= t < n_steps)
t = 3
t1 = t + 1

plt.figure(figsize=(8, 3.5))
plt.plot(times, positions, '-', markersize=8, alpha=0.8, label='Random walk (first 7 steps)')

plt.xticks(times)
plt.xlabel(f'Time (step={n_steps})')
plt.ylabel('Position')
plt.title('Random Walk -> Brownian motion')
plt.grid(alpha=0.3)
plt.tight_layout()
plt.show()
```

<img width="800" height="350" alt="image" src="https://github.com/user-attachments/assets/59ff5dae-9240-4ae9-a7b7-737bc16f4278" />


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
