# Dockerized Elixir/Phoenix Development Environment

### Introduction

This dockerized phoenix environment based on https://github.com/nicbet/docker-phoenix


#### Initialize the Database with Ecto

When you first start out, the `db` container will have no databases. Let's initialize a development DB using Ecto:

```
./mix ecto.create
```

If you copied an existing application, now would be the time to run your database migrations.

```
./mix ecto.migrate
```

### Starting the Application

Starting your application is incredibly easy, you can either run:

```
docker-compose up
```

or

```
./mix phx.server
```

Once up, it will be available under http://localhost:4000.

You may need to update `config/dev.exs` and set the endpoint listen address to `0.0.0.0` like so:

```
config :hello_world, HelloWorldWeb.Endpoint,
  # Binding to loopback ipv4 address prevents access from other machines.
  # Change to `ip: {0, 0, 0, 0}` to allow access from other machines.
  http: [ip: {0, 0, 0, 0}, port: 4000],
  check_origin: false,
  code_reloader: true,
  debug_errors: true,
  secret_key_base: "rM/QJOrRiW+3WWLw+lHJ8kUFJK/LTrwakSG/ftGYl8jYN0FKqfgS50l2C9BdKMoK",
  watchers: [
    # Start the esbuild watcher by calling Esbuild.install_and_run(:default, args)
    esbuild: {Esbuild, :install_and_run, [:default, ~w(--sourcemap=inline --watch)]}
  ]
```

## Notes

### Executing custom commands

To run commands other than `mix` tasks, you can use the `./run` script.

```
./run iex -S mix
```
