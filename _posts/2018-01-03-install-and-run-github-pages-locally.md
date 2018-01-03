---
type: post
title: "Install and run GitHub Pages locally"
---

This site is powered by Jekyll & GitHub Pages.

To run your own copy locally install ruby & bundler:
```bash
sudo apt-get update -y
sudo apt-get install -y ruby ruby-dev zlib1g-dev
sudo gem install bundler
```

Install git:
```bash
sudo apt-get install -y git
```

Clone site repository locally:
```bash
git clone https://github.com/adrianharabula/adrianharabula.github.io.git
```

Install necessary GitHub Pages dependencies:
```bash
cd adrianharabula.github.io
bundle install
```

Serve your own copy locally:
```bash
bundle exec jekyll serve
```

Now site is accesible locally at [localhost:4000](http://localhost:4000).

### Future work
 * Automate dependencies installation with Docker.
 * Make a demo how to make a pull request to update site
