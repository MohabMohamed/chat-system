# Contributing to Chat system

The goal of this file is to make contributing to this project as easy and transparent as possible.

---

## Pull requests

- Clone the repo and run `git submodule init && git submodule update`.
- Create your branch from master with `feature/name` or `issue/name`.
- If you've added code that should be tested, add tests.
- If you've changed APIs, update the documentation.

## Coding Style

- Don't overwrite any of the pre-commits
- Run rupocop in the rails directory and gofmt go directory before adding your code to staging.
- Test everything

## Setting up

- Clone the repo using `git clone git@github.com:MohabMohamed/chat-system.git`

- Install [ruby](https://www.ruby-lang.org)
  
- Install [go](https://golang.org/)

- Install [Docker](https://docs.docker.com/install/)

- Install [Docker compose](https://docs.docker.com/compose/install/)

- If you are working on the go service only without being a submodule enable the pre-commits by `go install github.com/go-courier/husky/cmd/husky && husky init`
  
- If you are working on the rails service only without being a submodule enable the pre-commits by `gem install overcommit && overcommit --install`

- Run `cp rails-chat-service/config/envfiles/example.env rails-chat-service/config/envfiles/production.env`
  
- Do it for `development.env` and `test.env` also

- Run `cp go-chat-service/config/example.env go-chat-service/config/production.env`
  
- Do it for `development.env` and `test.env` also
  
- Change the `.env` to have your environment variables
  
- Run `docker-compose -f docker-compose.dev.yml up`
