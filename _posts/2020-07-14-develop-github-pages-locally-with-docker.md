---
layout: post
title: Develop Github Pages locally with docker
---

[The official github pages documentation][1] explains how you can test your Github Pages using Jekyll locally. I had a hard time installing all dependencies. A faster and easier way is to use the [docker image provided by Jekyll][2]. Make sure you are using the image with the **pages** tag: `jekyll/jekyll:pages`.

I use below docker-compose file to start up an docker image with Jekyll which serves the current directory where I cloned my Github pages repository

```yaml
version: '3'
services:
    github-pages:
      image: jekyll/jekyll:pages
      volumes:
        - .:/srv/jekyll
      ports:
        - 4000:4000
      command: jekyll serve
```

[1]: https://docs.github.com/en/github/working-with-github-pages/testing-your-github-pages-site-locally-with-jekyll
[2]: https://hub.docker.com/r/jekyll/jekyll/