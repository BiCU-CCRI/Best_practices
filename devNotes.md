# How to's:

- Add .md pages in `docs` and add the links to them in `mkdocks.yml`.
- To add figures and onther things put in into `data`. Linkage in an MD file is done by `![](data/images/000_terminals_alternatives.png){width="678"}`
- Documentation for MkDocs-Materials is here: https://squidfunk.github.io/mkdocs-material/getting-started/
- Documentation for Base MkDocs is here: https://www.mkdocs.org/getting-started/
- Md Syntax: https://www.markdownguide.org/basic-syntax/
- useful thing to have - Markdown All in One pluging for VSCode
- launch the interactive server `docker run --rm -it -p 8000:8000 -v ${PWD}:/docs squidfunk/mkdocs-material`
- To connect to a site use this ip: `http://10.5.1.157:8000/`