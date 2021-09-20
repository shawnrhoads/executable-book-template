# Figure 1

This page contains supplemental interactive Python code for the following project:

<blockquote>Rhoads, S. A. (2021). An executable notebook template to enhance interactivity with research objects. The Journal of Examples.</blockquote>
<br>

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.css" integrity="sha512-5A8nwdMOWrSz20fDsjczgUidUBR8liPYU+WymTZP1lmY9G6Oc7HlZv156XqnsgNUzTyMefFTcsFH/tnJE/+xBg==" crossorigin="anonymous" />

<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.3.4/require.min.js"></script>

<script type="text/x-thebe-config">
     {
       requestKernel: true,
       binderOptions: {
         repo: "matplotlib/ipympl",
         ref: "0.6.1",
         repoProvider: "github",
       },
     }
</script>
<script src="https://unpkg.com/thebe@latest/lib/index.js"></script>
   
<button id="activateButton" style="font-size: 1em;">
    Click here to interact with the code
</button>

<script>
var bootstrapThebe = function() {
   thebelab.bootstrap();
}
document.querySelector("#activateButton").addEventListener('click', bootstrapThebe)
</script>
<br>

## Figure 1

<pre data-executable="true" data-language="python">
# interactive display
import matplotlib.pyplot as plt
import ipywidgets as widgets
import numpy as np

# set up data
x0_viz = np.ones((131, 1))
x1_norm = np.random.normal(loc=54.9,scale=30.1,size=(131,1))
x1_viz = x1_norm - min(x1_norm)
X_viz = np.hstack((x0_viz, x1_viz))
noise_viz = np.random.normal(2, 10, (131,1)) 
y_viz = 347 - 1.75 * x1_viz + noise_viz

@widgets.interact(beta_hat=widgets.FloatSlider(-1.75, min=-3, max=0),
                  intercept=widgets.FloatSlider(347, min=100, max=400))
def plot_data_estimate(intercept, beta_hat):
    # compute error
    X, y = X_viz, y_viz
    y_hat = (intercept*X[:,0] + beta_hat*X[:,1]).reshape(len(y),1)
    MSE_val = np.mean((y - y_hat)**2)
    
    # plot
    fig, ax = plt.subplots()
    ax.scatter(X[:,1], y, label='Observed')  # our data scatter plot
    ax.plot(X[:,1], y_hat, color='r', label='Fit')  # our estimated model

    # plot residuals
    ymin = np.minimum(y, y_hat)
    ymax = np.maximum(y, y_hat)
    ax.vlines(X[:,1], ymin, ymax, 'g', alpha=0.5, label='Residuals')

    ax.set(
        title=f"intercept={intercept:0.2f}, beta = {beta_hat:0.2f}, MSE = {MSE_val:.2f}",
        xlabel='x',
        ylabel='y')
    
    ax.legend()
    plt.show()
</pre>