# NARB - NGINX Amazing Redirect Bullshit
A simple link shortener using NGINX redirects, written with 28 lines of Bash.

## Requirements

- NGINX web server
- SSH

## Setup

Because of it's simplicity, this utility requires a fair bit of setup.

#### 0. SSH & clone
This tool uses `ssh` so make sure to properly setup your SSH keys. Then clone this repo.

#### 1. Edit NGINX config
In your NGINX config file (commonly located in `/etc/nginx/sites-available/`) add a `# REDIRECT` comment where you want the redirects to be appended. Example below:

```
server {

    root /srv/www/link.chamik.eu;

    index index.html;

    # REDIRECT

    server_name link.chamik.eu www.link.chamik.eu;

    ...
```

#### 2. Edit `narb-server`
Change the variables at the top of the file to reflect the correct information.

```sh
NGINX_CONFIG="/etc/nginx/sites-available/link.chamik.eu"
URL="https://link.chamik.eu"
```

#### 3. Edit `narb`
Edit the user and host to reflect the correct information.

```sh
ssh kubik@link.chamik.eu /usr/local/bin/narb-server "$@"
```

#### 4. Deploy
Add each script to their respective PATH.

```sh
scp narb-server chamik@example.com:/usr/local/bin/
cp narb /usr/local/bin/
```

And you're done!

## Usage

You have 3 very simple commands at your disposal.

#### add [LINK] [TARGET] - Create a new redirect

```
$ narb add dogs https://www.omfgdogs.com/
Added redirect from https://link.chamik.eu/dogs to https://www.omfgdogs.com/
```

#### remove [LINK] - Remove a redirect

```
$ narb remove dogs
Removed the https://link.chamik.eu/dogs redirect
```

#### list - List all current redirects

```
$ narb list
rickroll -> https://www.youtube.com/watch?v=9rmBqIFeHN8 
google -> https://google.com
```

## Other stuff

Thanks [@mariansam](https://github.com/mariansam) for coming up with this and creating the orignal script.

I've tested this with only about 10 redirects set up and it was pretty snappy. I am not sure what happens if you have *dozens* of them. This is only meant as a simple solution for only a handful of redirects.