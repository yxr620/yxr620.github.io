# Blog

Personal academic/blog website built with [Hugo](https://gohugo.io/) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme.

## Commands

```bash
# Start local dev server (localhost only)
hugo server

# Start dev server accessible on local network (replace <your-server-ip> with your machine's IP)
hugo server --bind 0.0.0.0 --baseURL http://<your-server-ip>:1313

# Build the site locally (output goes to ./public, which is ignored by Git)
hugo

# Create a new blog post
hugo new blog/<post-name>/index.md
```

## Deployment

Push the `main` branch to trigger `.github/workflows/hugo.yaml`. GitHub Actions builds the site and deploys the generated artifact to GitHub Pages at <https://yxr620.github.io>.
