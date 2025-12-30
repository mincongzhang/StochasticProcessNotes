```
https://python-fiddle.com/examples/matplotlib?checkpoint=1767058952
```


```
import numpy as np
import matplotlib.pyplot as plt

# Parameters / reproducibility
np.random.seed(42)
N = 300
epsilon = 150  # larger horizontal distance for visibility

# Generate a 1D random walk (x = time/index, y = cumulative sum of steps)
x = np.arange(N)
steps = np.random.normal(loc=0.0, scale=1.0, size=N)
y = np.cumsum(steps)

# Pick two points whose x-index distance is <= epsilon
i = np.random.randint(0, N - epsilon)          # starting index
delta = np.random.randint(1, epsilon + 1)      # choose how far ahead (1..epsilon)
j = i + delta

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

# Label the two points as requested, make them bold and larger
plt.annotate(r"$\mathbf{B(t)}$", xy=(x[i], y[i]), xytext=(-10, 12),
             textcoords='offset points', ha='right', va='bottom', color='red',
             bbox=dict(facecolor='white', edgecolor='none', alpha=1),
             fontsize=16, fontweight='bold')
plt.annotate(r"$\mathbf{B(t+\epsilon)}$", xy=(x[j], y[j]), xytext=(8, -10),
             textcoords='offset points', ha='left', va='top', color='red',
             bbox=dict(facecolor='white', edgecolor='none', alpha=1),
             fontsize=16, fontweight='bold')

# Label slope "A" near the midpoint, rotated to match slope
midx, midy = (x[i] + x[j]) / 2, (y[i] + y[j]) / 2
angle = np.degrees(np.arctan(A))
plt.text(midx, midy, "A \n\n", color='red', weight='bold', fontsize=18,
         bbox=dict(facecolor='white', edgecolor='none', alpha=1),
         rotation=angle, ha='center', va='center')

# Expand axis ranges for better view
x_margin = int(N * 0.10)
y_span = y.max() - y.min()
y_margin = y_span * 0.12
plt.xlim(x.min() - x_margin, x.max() + x_margin)
plt.ylim(y.min() - y_margin, y.max() + y_margin)

plt.xlabel('Index (x)')
plt.ylabel('Walk position (y)')
plt.title(f'Random walk with two points within epsilon={epsilon} (indices {i} and {j})')
plt.legend()
plt.grid(alpha=0.3)
plt.tight_layout()
plt.show()
```

<img width="1200" height="600" alt="image" src="https://github.com/user-attachments/assets/36746c44-ea3f-42e1-a595-e1ab60e60062" />
