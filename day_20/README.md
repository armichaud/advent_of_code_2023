Solved part 1

I dumped a lot of time into a solution where each individual pulse module had a reference to the event queue, keeping track of its own subscribers. It required use of smart pointers with runtime borrow checking, and the whole thing broke immediately because there were multiple mutable borrows of the manager. Maybe someone more familiar with Rust could have figured out how to make this work, but I was largely inspired by the architecture of a PyGame program I dabbled with a long time ago. 

I solved part 1 by refactoring so that the manager was its own struct and was responsible for the publisher/subscriber relationships. I still feel like the input parsing could be more succinct, but whatever.

Part 2 seems to be to large for just running the program. I'm mostly giving up here because I don't have more time to sink into this, but my general thoughts are this:
- Work backwards from the output, determining how many button presses would be required for the input to eventually pass on a low signal to RX.
- The tricky part is that every conjunction module demands that you assess the cycles that every single input goes through, finding when they each send a High signal and then finding when those are all aligned using the LCM of all their cycle lengths. 
- In theory, I think you can work back to the broadcaster, with the LCM of the number of times its outputs each need to receive a low pulse.