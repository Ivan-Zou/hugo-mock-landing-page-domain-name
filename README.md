# Voice Tech Collar
A technological collar that enhances one's voice

## Description of Auto Deploying Workflow
```name: 🏗 Build and Deploy GitHub Pages```

This line sets the name of the workflow, which will be displayed on the GitHub Actions UI.
```on:
push:
branches:
- main
```

This section specifies the event that will trigger the workflow. In this case, the workflow will run whenever
code is pushed to the main branch.
```jobs:
deploy:
runs-on: ubuntu-22.04
This section defines a job called deploy that will run on an Ubuntu 22.04 runner.
steps:
This line starts the definition of the steps that will be executed in the deploy job.
- name: 🔄 Check Out Source Repository
uses: actions/checkout@v3.5.1
with:
submodules: true # Fetch Hugo themes (true OR recursive)
fetch-depth: 0 # Fetch all history for .GitInfo and .Lastmod
This step checks out the repository's code, including submodules (e.g., Hugo themes), and fetches the entire
commit history to ensure proper Git information and last modification dates.
- name: 🛠 Initialize Hugo Environment
uses: peaceiris/actions-hugo@v2.6.0
with:
hugo-version: "0.123.4"
extended: true
```

This step sets up the Hugo environment by installing the specified version (0.123.4) of Hugo with the
extended mode enabled.
```
- name: 🏗 Compile Hugo Static Files
run: hugo -D --gc --minify
```
This step runs the hugo command to compile the static website files. The -D flag includes content marked as
draft, --gc enables garbage collection, and --minify minifies the output.
```
- name: 🚀 Publish to GitHub Pages
uses: peaceiris/actions-gh-pages@v3.9.3
with:
github_token: ${{ secrets.GITHUB_TOKEN }}
publish_branch: gh-pages
user_name: "github-actions[bot]"
user_email: "github-actions[bot]@users.noreply.github.com"
```
This step publishes the compiled website to the gh-pages branch, which is used by GitHub Pages to serve
the website. It uses the peaceiris/actions-gh-pages action and sets the required github_token secret,
the destination branch (gh-pages), and the user name and email for the Git commit.
```
## NOTE: uncomment below if using a custom domain
## cname: mydomain.com
```
These lines are commented out but provide instructions for specifying a custom domain if needed.
In summary, this GitHub Actions workflow checks out the repository, sets up the Hugo environment, compiles
the static website files using Hugo, and publishes the compiled files to the gh-pages branch, which is used
by GitHub Pages to serve the website.
