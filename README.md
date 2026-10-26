# Adaptive Optimizer Playground

An interactive classroom demo for **Algorithms with Adaptive Learning Rates** in Deep Learning Module 4. It animates SGD, AdaGrad, RMSProp, and Adam over the same two-parameter loss surface, with a live loss chart and controls for learning rate, surface, and update budget.

## Run it

Open [`index.html`](index.html) in Chrome, Edge, or Firefox. No Python, installation, account, or internet connection is needed. For a local server, run `python -m http.server 8000` and visit `http://localhost:8000`.

## Classroom walkthrough (about 3 minutes)

1. Select **Narrow valley** and keep the defaults. Ask the audience which colored path they expect to be smoothest.
2. Press **Run race**. Point to the contour trajectories and the loss curves below. Each dot is a pair of model parameters; darker central regions indicate lower loss.
3. Explain that SGD uses the current gradient, AdaGrad accumulates squared gradients, RMSProp uses a moving average of squared gradients, and Adam also tracks gradient momentum.
4. Change the learning rate, then rerun. Ask why the paths change. Switch to **Balanced bowl** to show that optimizer behavior depends on the geometry.

The **Step once** button is useful when explaining the direction of a single update. **Reset** returns every method to the identical initial coordinates.

## What the visuals mean

The contour background is a top-down picture of loss as two parameters change. The colored trails are the actual updates calculated by the algorithms. The chart plots their loss after each update; lower is better. Each run shares the same starting point, surface, base learning rate, and number of updates.

| Optimizer | Stored history | Update idea |
| --- | --- | --- |
| SGD | None | Move against the current gradient. |
| AdaGrad | Sum of all earlier squared gradients | Divide each coordinate's gradient by its accumulated scale. |
| RMSProp | Exponential average of squared gradients | Scale using recent gradient magnitudes. |
| Adam | Exponential averages of gradients and squared gradients | Use momentum and per-coordinate scaling with bias correction. |

Defaults: RMSProp decay 0.9; Adam β₁ = 0.9, β₂ = 0.999; numerical epsilon = 1e-8. SGD here is plain SGD without momentum. All updates are implemented in the inline JavaScript of `index.html`.

## Scope

This is a **toy two-parameter optimization problem**, not neural network training. The narrow valley and balanced bowl are quadratic surfaces; the bumpy surface adds cosine ripples and can have local minima. Comparing optimizers at the same numeric base learning rate is illustrative, not a tuned or statistically controlled benchmark. A different starting point, learning rate, surface, or tuning procedure can change the outcome. Adaptive optimizers also do not guarantee the best generalization on real data.

## Project structure

`index.html` contains the complete responsive demo, optimizer updates, and visualizations. `README.md` is the presentation and usage guide. There are no external dependencies.
