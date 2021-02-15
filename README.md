# use_env_dir

`use_env_dir` is a function for `direnv`.

It loads environment variables one par file under the `.direnv/env` directory.

This functionality is very similar to which is seen in [Heroku Buildpack](https://devcenter.heroku.com/articles/buildpack-api#bin-compile).

Each file under the "env_dir" represents an environment variable, whose filename to be the variable's name and content to variable's value.

So the file with the name `DB_PORT` and the content `32800` will turn to an environment variable of `DB_PORT=32800`.

## How to use

Add the following line to your `~/.config/direnv/direnvrc`:

```sh
source_url "https://raw.githubusercontent.com/kayhide/direnv-use-env-dir/master/use_env_dir.sh" "sha256-jaaRik1JVXwgTQFWOr15WVY1OvYcVt+Oek9l3d85lUY="
```

Then in any `.envrc`, put the following line:

```sh
use_env_dir
```

## Use case

One use case of this functionality is to launch a database server container by docker-compose and let it to pick any available port.
You can fill `DB_PORT` by creating a corresponding file as:

```console
$ mkdir -p .direnv/envs
$ docker-compose port db 5432 | cut -d ':' -f 2 > .direnv/envs/DB_PORT
```

And make your application to read the `DB_PORT`.

In this way, you can access the db without worrying about port conflict, no matter how many similar projects you are working on in parallel.
