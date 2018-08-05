# pong-plus-plus

A reinforcement learning method for teaching a computer to play pong in MATLAB. Submitted by Matt Dickson, Jeff Ermyer, and Botao Hu for the
MathWorks intern hackathon 2018.

## Input
Prepared by Botao and Jeff, the input is a 1-by-14 vector containing the ball's x and y location, the paddle's location, ball speed, etc. Feature scaling was applied
outside the network before passing them in.

## Learning
Prepared by Matt.
### Neural Network
The neural network has one hidden layer of 200 nodes and one node in the output layer, with activation of the out representing the probably that the paddle should 
move up. The network uses vectors and matrices to represent it's internal state, allowing for a highly vectorized process for forward and backward propagation. 

### Rewards and Punishments
The algorithm is reward for lasting a longer than average time against its opponent rather than by wins/losses since its training partner is theoretically unbeatable -- it 
just tracks the y coordinate of the ball. The network stores how long it took to lose to its opponent and compares that to its average thus far, rewarding or punishing itself 
based on the z-score of the current round minus a small additional, constant penalty. This small extra punishment helps to break the algorithm of early behavior, as it ensures
that doing only average will slowly force it to try new strategies, but does mean this model tends to oscillate around its best possible state rather than strictly converge to 
a single value. 

## Picture
![](https://gph.to/2vjX4Vn)

## Notes
This model learned to only care about the y coordinate of the ball and the current paddle coordinates,just as the cheating model does. There's no reason this network couldn't 
use a down-sampled image to learn with, however, we just chose not to do this since it made the game run extremely choppy. A more optimized figure generating approach could 
allow this network to be used on a visual input instead.
 