#Network Optimizers Summary!


## Gradient descent-

    x += -learning_rate * dx

### Remarks- 
Wont work nicely when the data's gradient is not same along different bases of the vector space.

## Momentum Update-

    v = mu * v - learning_rate * dx
    x += v

### Remarks - 
* Allows building up velocity in shallow directions (bases which have less component of gradient vector).
* Also, dampens the momentum in steep directions.

## Nesterov Momentum

    v_prev = v
    v = mu * v - learning-rate * dx
    x += -mu*v_prev + (1 + mu) * v

### Remarks - 

* Also known as the "look ahead" gradient, i.e., first it calculates the next step based only on momentum and thentakes the gradient step from this lookahead position. 

## Adagrad (Element - Wise scaling) - 

    cache += dx**2
    x += - learning_rate * dx / (sqrt(cache) + 1e-7)

### Remarks - 
* Working in a way different from Momentum, but in a different way.
* Scales up and down the update steps according to the mmagnitude of gradient in different directions (or bases).
* Also, learning rate decays to zero as the cache is increasing!

## RMS Prop- 

    cache = decay_rate * cache + (1 - decay_rate) * dx**2
    x += learning_rate * dx / (sqrt(cache) + 1e-7)

### Remarks- 
* The decay introduced provides a kind of leaky effect to the decay rate.
* Ends up forgetting gradients from a long time ago.

## Adam ('Adagrad and Momentum')-

    # Beta Version-
    m = beta1*m + (1 - beta1) * dx  ## Momentum
    v = beta2*v + (1 - beta2) * (dx**2)
    x += - learning_rate * m / (np.sqrt(v) + 1e-7) ## RMS Proplike function


    # Full Version-
    m, v = .. # ~0 for most cases
    for t in range(1, num_iterations):
        m = beta1*m + (1 - beta1) * dx  ## Momentum
        v = beta2*v + (1 - beta2) * (dx**2)
        fub = m / (1 - beta1 ** t)
        sub = v / (1 - beta2 ** t)
        x += - learning_rate * m / (np.sqrt(v) + 1e-7)

### Remarks - 
* Combines the effect of both momentum and rmsprop.
* Bias correction for the fact that first and second moment 
estimates are initialized as zero.