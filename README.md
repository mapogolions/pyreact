## Pyreact event loop


It's modest attempt to implement the reactor pattern to break the traditional synchronous flow. The event loop uses a single thread and is responsible for scheduling asynchronous operations.


### Introduction

In JS event loop is available out of the box. It is working behind the scenes. Asynchronous code in JS looks like this:

```js
setTimeout(() => console.log('world!'), 1000);
console.log("Hello ");
```

the same things with `pyreact-event-loop`:

```python
loop = event_loop.SelectLoop()
loop.add_timer(1, lambda: print("world!"))
print("Hello ")
loop.run()
```

In python needs to explicitly define the event loop.


### ... by standing on the shoulders of Giants

`Pyreact-event-loop` based on `ReactPHP event loop` component.

There are three available implementations:

* `SelectLoop` uses the [`select`](https://docs.python.org/3/library/select.html) module
* `LibevLoop` uses the [`mood.event`](https://github.com/lekma/mood.event) python `libev` interface
* `LibuvLoop` uses the [`pyuv`](https://github.com/saghul/pyuv) python interface for `libuv`


[For more details see](https://reactphp.org/event-loop/)

### Examples

* [timers](./examples/01-timers.md)
* [periodic timers](./examples/02-periodic.md)
* [ticks](./examples/03-ticks.md)
* [signals](./examples/04-signals.md)
* [echo server](./examples/05-echo-server.md)
* [fp streams](./examples/06-fp-streams.md)

### How to use

```sh
(env) $ git clone <url>
(env) $ cd project
(env) $ pip install -r requirements.txt
(env) $ pytest
(env) $ python setup.py install
(env) $ python
>>> import event_loop
>>> loop = event_loop.SelectLoop()
>>> loop.add_periodic_timer(2, lambda: print('tick'))
>>> loop.run()
```
