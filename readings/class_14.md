## DATA VISUALIZATION

### Matplotlib

Prep:

    import numpy as np

    X = np.linspace(-np.pi, np.pi, 256, endpoint=True)
    C, S = np.cos(X), np.sin(X)

Changing colors and line widths:

- `plt.figure(figsize=(10,6), dpi=80)`
- `plt.plot(X, C, color="blue", linewidth=2.5, linestyle="-")`

Setting limits:

- `plt.xlim(X.min()*1.1, X.max()*1.1)`
- `plt.ylim(C.min()*1.1, C.max()*1.1)`

Setting ticks:

- `plt.xticks( [-np.pi, -np.pi/2, 0, np.pi/2, np.pi])`
- `plt.yticks([-1, 0, +1])`

Setting tick labels:

- `plt.xticks([-np.pi, -np.pi/2, 0, np.pi/2, np.pi], [r'$-\pi$', r'$-\pi/2$', r'$0$', r'$+\pi/2$', r'$+\pi$'])`
- `plt.yticks([-1, 0, +1], [r'$-1$', r'$0$', r'$+1$'])`

Moving spines (removing op and right, moving bottom and left to the center):

    ax = plt.gca()
    ax.spines['right'].set_color('none')
    ax.spines['top'].set_color('none')
    ax.xaxis.set_ticks_position('bottom')
    ax.spines['bottom'].set_position(('data',0))
    ax.yaxis.set_ticks_position('left')
    ax.spines['left'].set_position(('data',0))

Adding a legend:

    plt.plot(X, C, color="blue", linewidth=2.5, linestyle="-", label="cosine")
    plt.plot(X, S, color="red",  linewidth=2.5, linestyle="-", label="sine")

    plt.legend(loc='upper left', frameon=False)

Annotate some points:

    t = 2*np.pi/3
    plt.plot([t,t],[0,np.cos(t)], color ='blue', linewidth=1.5, linestyle="--")
    plt.scatter([t,],[np.cos(t),], 50, color ='blue')

    plt.annotate(r'$\sin(\frac{2\pi}{3})=\frac{\sqrt{3}}{2}$',
             xy=(t, np.sin(t)), xycoords='data',
             xytext=(+10, +30), textcoords='offset points', fontsize=16,
             arrowprops=dict(arrowstyle="->", connectionstyle="arc3,rad=.2"))

    plt.plot([t,t],[0,np.sin(t)], color ='red', linewidth=1.5, linestyle="--")
    plt.scatter([t,],[np.sin(t),], 50, color ='red')

    plt.annotate(r'$\cos(\frac{2\pi}{3})=-\frac{1}{2}$',
             xy=(t, np.cos(t)), xycoords='data',
             xytext=(-90, -50), textcoords='offset points', fontsize=16,
             arrowprops=dict(arrowstyle="->", connectionstyle="arc3,rad=.2"))

### Bokeh

    from bokeh.plotting import figure, output_file, show

    x = [1, 2, 3, 4, 5, 6]
    y = [4, 2, 1, 3, 6, 8]

    output_file('index.html')

    # Add plot
    p = figure(
        title='Simple example',
        x_axis_label='X Axis',
        y_axis_label='Y Axis',
    )

    # Render glyph
    p.line(x, y, legend='Test', line_width=2)

    # Show results
    show(p)

[Go back](../README.md)
