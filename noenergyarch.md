An embedded Computer Architecture ideas that work forward
a goal when power is available and stop working when not.

Should not handle power loss by agressive use of batteries,
but by providing architecture that handles the case in a
well degenerating way so that it can continue.

Basically it is just about some certain philosophies:

* Redoability: The property of a hardware architecture if it only contains operations that one can run twice and get the same result.

* Persistence: The architecture should work with persistent elements - eink displays, ferroelectric memories, etc

* Transactionality: Stepping ahead with the instruction pointer is transactional and is happening above a redoable operation

* Controlled PLOD (possible loss of data): There can be a way to support bigger chunks of non-transactional and non-redoable fast code or I/O as one-liner calls in the architecture, but the end result of theirs should be quasi-transactional.

* Inverted-control-communications: output devices should store state generally, input devices should be processed in a way that it does not count to have a data loss. This way whole states are transferred and checking result of a change should be pollable to the sending side any time soon after the operation. In human I/O this is the easiest as if power goes down right on button presses and thus a keystroke is lost, we humans can handle that. When using M2M communications the things get to be harder...

* Ask-to-download-communications: When senders want the system to get some data over a network it is much better to just tell them in very small messages where the data is and let the embedded system download it using redoable operations internally. This way only the small message can get lost, for which there is only a small chance.

This is a very tricky architecture, most easily implemented by a custom microcontroller firmware that ensures all the above (and more) rules by acting as an interpreter over a ferroelectric or similar memory.
