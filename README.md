# EnID Documentation Proof of Concept
- Static Site Generator: MkDocs
- Material Design Theme (V4.60) for MkDocs (V5 brings more  customizing possibilities)

# Access
- Github Repo: https://github.com/1701/d
- Rendered MkDocs HTML output on Github Pages: https://doc.appmazing.net

# Structure
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


