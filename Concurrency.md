
```verse
Concurrency := module:

```
# A parametric interface implemented by events with a `payload` that can be waited on. Matched with `signalable.`

```verse
    awaitable<public>(payload:type) := interface:

```
        # Suspends the current task until resumed by a matching call to `signalable.Signal`. Returns the event `payload`.

```verse
        Await<public>()<suspends>:payload

    awaitable<public>() := awaitable(void)

    task<native><public>(t:type) := class<abstract><final>(awaitable(t)):
        Await<native><override>()<suspends>:t

...


```
