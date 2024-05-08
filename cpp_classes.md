BasicSlot: 
- a templated function holder, similar to `std::function`?  
- uses `bind()` to initialise the callback

CyclTime: (why not CycleTime?)
- provides 'clock' functionality like `now()`
- has a monotonic clock and wall clock internally

Epoll:  
- an utility to call `epoll_` functions from standard library

EventFd:  
- an utility to handle file descriptors  
- has members that calls `read()` and `write()` from standard library

Hook:  
- wraps around `BasicSlot` to be able to insert it into `boost::intrusive::list`

Initiator: (CRTP `: public StreamConnector<Initiator>`)
- represents a socket stream connection?
- handles session events and socket events

Reactor:  
- reacts to file descriptors being ready
- `poll()` member function waits for ready descriptors (`epoll_wait`), then invokes corresponding callbacks (wrapped inside `Timer`)

Resolver:
- translates URI to `addrinfo`
- runs in a thread, uses `std::future` to pass results

Runner:   
- runs 'things' in a separate thread  
- a thread-safe stop token to notify the thread to exit

TimerQueue:
- a sorted (by expiry time) list of timers
- when a timer expires (`expiry_time < now`) it will invoke the callback stored as `TimerSlot` (see `BasicSlot`)
