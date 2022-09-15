# Personal Blog and Portfolio


## Running with Jekyll

```bash
bundle install
bundle exec jekyll serve
```

## Running with Docker

### Pre-requisite

 - Install Docker

### Steps to Run

```bash
git clone https://github.com/rehanguha/rehanguha.github.io.git
cd rehanguha.github.io.git
```

```bash
docker run --rm --volume="$PWD:/srv/jekyll" -e JEKYLL_UID=1001 -e JEKYLL_GID=116 -p 4000:4000 rehanguha/jekyll:blog-v1.0 jekyll serve
```

Check out the blog at `http://localhost:4000`

