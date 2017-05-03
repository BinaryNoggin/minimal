# Minimal

This is to show an issue that I ran into where a module is available
locally but not on the device. It can be tested with this application.

[Repo](https://github.com/BinaryNoggin/grove/tree/huh)

## Issue

```elixir
def deps do
  [{:minimal, path: "path/to/minimal"}]
end
```

In project including this

Start iex on the host `MIX_TARGET=host iex -S mix`

```elixir
  iex(1)> Minimal.hello
  :world
```

Deploy to the target device `MIX_TARGET=bbb mix do firmware, firmware.burn`


```elixir
  iex(1)> Minimal.hello
  ** (UndefinedFunctionError) function Minimal.hello/0 is undefined (module Minimal is not available)
      Minimal.hello()
```

Go back to the mix config and add minimal to your applications.

```elixir
applications: [:nerves_interim_wifi, :minimal],
```

Reburn the firmware.
Now doing the same thing on the device.

```elixir
  iex(1)> Minimal.hello
  :world
```

## Question

Why does the module show up on the host console, but not on the device
console unless added to the list of applications?
