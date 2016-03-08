# Rawkode's Docker Tooling Helpers

## Installing
1. Clone the repository to your local machine.
2. Add the directory to your path

## Naming

Yes - the scripts have terribly explicit names. Alias away!

## Syncing files to docker-machine

On OSX and find VBoxFs too slow? Indeed :/

Create your machine with `--virtualbox-no-share` and use `docker-machine-rsync` to replicate your local directory on the virtual-machine with rsync!

You can run this once per project, within your project - or in your home directory to support multiple projects.

Don't want to sync .git directories? Of course not. Create `.rsyncignore` in the directory you plan to run the command and omit whatever you want:

### .rsyncignore
```
.git
cache/*
tmp/*
log/*
logs/*
```

## Run an arbitrary command in any of your compose services

Inside of a project that is utilising docker-compose:

```
$ docker-compose-run-command whoami

Executing ... [ Environment:  ] on container 'application'  'whoami'

root

$
```

Don't want to run the command using your 'application' service, or as root? No problem:

```
$ docker-compose-run-command -u www-data -s httpd whoami

Executing ... [ Environment:  ] on container 'httpd'  'whoami'

www-data
```

### Are you extending compose files? You filthy animal!

Use the environment toggle! `-e test` and `-d` to show debug output, that displays the command being run:

```
Executing ... [ Environment: test ] on container 'application'  'whoami'

[ Debug ] Executing command: docker-compose -f docker-compose.yml  -f docker-compose.test.yml  run  --entrypoint='sh -c ' application 'whoami'

root

```
