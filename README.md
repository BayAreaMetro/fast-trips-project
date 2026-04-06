Fast-Trips Project Website
==========================

This repository contains the Jekyll site for the Fast-Trips project.

## Site URL

- Production: https://bayareametro.github.io/fast-trips-project/

## Prerequisites

- Ruby 3.2+ recommended
- Bundler (`gem install bundler`)

## Local development

1. Install dependencies:

	```bash
	bundle install
	```

2. Run the site locally:

	```bash
	bundle exec jekyll serve
	```

3. Open:

	- http://127.0.0.1:4000/fast-trips-project/

## Build for production

```bash
bundle exec jekyll build
```

Build output is written to `_site/`.

## Deployment

Deployment is handled by GitHub Actions in [.github/workflows/jekyll.yml](.github/workflows/jekyll.yml). Any push to `main` triggers a build and deploy to GitHub Pages.

## Repository organization

- Posts: `/_posts`
- Layouts: `/_layouts`
- Includes: `/_includes`
- Data files: `/_data`
- Custom plugin: `/_plugins/hex_to_rgb.rb`
- Images: `/img`
- Documents: `/library`

## Credits

Loosely based on the Agency theme:
http://startbootstrap.com/templates/agency/
