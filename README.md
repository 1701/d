# EnID Documentation Proof of Concept
- Static Site Generator: MkDocs
- Material Design Theme (V4.60) for MkDocs (V5 brings more  customizing possibilities)

# Access Documentation
- Rendered MkDocs HTML output on Github Pages: 
    - **https://doc.appmazing.net**
    - or: https://1701.github.io/d

# Project Structure
- Github Repo: https://github.com/1701/d
- Master Branch: 
    - docs
        - documentation pages (markdown)
        - Folder '/stylesheets/' (override theme preset)
        - Folder '/images/' (image files)
    - custom theme
        - main.html (override standard footer)
    - .gitignore
        - /site Folder
        - **/.DS_Store
- gh-pages Branch
    - MkDocs HTML Site Structure
      - git add/commit/push via 'mkdocs gh-deploy' command
    - CNAME file for custom domain settings

# Content Creation:
- Write new docs with Markdown: https://www.mkdocs.org/user-guide/writing-your-docs/
- Convert existing Word Document -> Markdown with pandoc:
    - command line: 'pandoc -f docx -t markdown foo.docx -o foo.markdown'
    - to save the images, add the option --extract-media=./ to the command above. It will create a folder 'media' with all the images and they will be correctly shown in the markdown file.
    - Make sure that the result of the automatic conversion is proper. 

# Mermaid -> Diagrams

The trick is:
- To include MermaidJS assets in your bundle
- to use Pymdown's Superfences extension to make mkdocs build "mermaid" code sections into div with the "mermaid" class.

This section is the relevant section of the doc: https://facelessuser.github.io/pymdown-extensions/extensions/superfences/#custom-fences

Mermaid Syntax: https://mermaid-js.github.io/mermaid/#/

``` shell
markdown_extensions:
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_div_format

extra_javascript:
  - https://unpkg.com/mermaid@8.4.6/dist/mermaid.min.js
```
