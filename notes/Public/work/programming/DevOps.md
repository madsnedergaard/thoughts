---
description: All knowledge related to DevOps and Cloud infrastructure. Probably a lot of things I missed
notetype: feed
date: 2022-01-10
status: seedling
tags: ["development"]
---

- General ideas


## Docker

- Docker tips & tricks & one-liners

### Cleaning up

```bash
# remove images older than 15 days
docker system prune --all --force --filter "until=360h" 

# remove dangling images and volumes
docker system prune --force --volumes 
```

### How to see content in docker images/containers

```sh
# images
docker run -it IMAGE sh

# containers
docker exec -it IMAGE sh
```


### Handy aliases
{% raw %}
```sh
alias docker-images-by-size="docker images --format '\{\{.ID}}\t{{.Size}}\t{{.Repository}}' | sort -k 2 -h"

alias docker-images-latest="docker images | head -n 10"
```
{% endraw %}

## Google Cloud Platform

- Cloud Run vs Cloud Functions

## Links

* [Setting up Cloud Scheduler to Trigger Cloud Run](https://benjamincongdon.me/blog/2019/11/21/Setting-up-Cloud-Scheduler-to-Trigger-Cloud-Run/)