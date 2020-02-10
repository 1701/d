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
