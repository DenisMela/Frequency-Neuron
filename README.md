# Frequency Neurons for Feedforward Neural Networks

The frequency neuron is a new artificial neuron I created that uses frequencies to produce weight values. Traditional artificial neurons in Feedforward neural networks use predetermined weight values, in this case weight values are determined by the duration of time the recieved input waits inside the neuron before being processed. This means in order to change the weight value for the recieved input, the input connection frequency should be changed. Every connection, both input and output, contains its own frequency for every neuron, therefore every connection contains its own set of produced weights.

You may be asking "How can this work if the network is designed in layers? Neurons would be activating with no input the moment the simulation starts". This is why each layer must start at a designated time, requiring the need for a new concept called sync layers. A sync layer is a collection of deactivated frequency neurons that has a delay time that starts counting the moment the network is active. Once the delay duration has ended, the sync layer activates the neurons it contains and they start recieving inputs and producing outputs. If a deactivated neuron recieves an input, that input is destroyed. Inputs only register when the neuron is active.

Since this neuron uses time as the weight variable, it's impossible to have a weight with a negative value. This is why the non-linear activation function used should be altered to only accept positive values (there can't be negative time).

Time based weight acumulation can also be non-liniar, so instead of increasing linearly by miliseconds the weight can be modified by a function to produce non-linear weight.

You might have asked "What happens to the input when the neuron outputs a value?" I have four ideas for this

- Either the input is destroyed once the neuron outputs the value to the connection, OR
- The input stays in the neuron, and accumulates more weight until every output connection has been sent a value, then it is destroyed or the neuron is deactivated.  OR
- The input stays in the neuron, but is reduced a certain amount (for example divide total weight by 2) then continue accumilating more weight normally. OR
- The input stays in the neuron, but is reduced a certain amount (for example divide total weight by 2) then continue accumilating more weight but the accumilation of weight is modified(increased/decreased speed of weight accuminlation for total input connections or even for specific ones)

This is how a Feedforward network can be designed using frequency neurons. 


A good questions is "How would anyone train this kind of network?" If you set each connection to fire only once, and have each sync layer a delay of 12 seconds consecutively, and the input value for all connections is 1, the maximum weight value any connection can have is 11.999. If you're using an altered sigmoid activation function, a single connection in this example is enough to result in an output of 0.999999. But lets say each neuron has 6 input connections and the sync layer delay time is 2, if all connections recieve an input the moment the sync group activates, the output for each neuron would also be 0.999999 even though the maximum weight value for each connection is 1.9999 and the input value is 1.

Something different this neuron can do compared to traditional Feedforward neurons is this neurons ability to scale weights based on time. The longer the inputs wait in the recieving end of a neuron, the larger the weight becomes. This means not only can weights be changed by the input frequency of each connection, but the output frequency can determine the total weight values of all its inputs.

This network also has the ability to send the same input multiple times, with each repeated input having it's own weight value that is multiplied together before being summed to produce the final input value for that connection and in total all connections in that neuron. 

Any Basic Feedfoward network can be converted into a network that impliments frequency neurons by:
- Converting hidden layers into sync layers (add a delay time that is consecutive to eachother so they don't all activate at the same time. For example 4, 8, 12, 16), 
- Create a frequency for each neuron connection
- Every neuron connection may only fire once
- Change the activation function to use only positive input values
- Deactivate the neuron once it has sent a signal to all of its output connections
- Have the network operate in real time (for weights, sync layers)



