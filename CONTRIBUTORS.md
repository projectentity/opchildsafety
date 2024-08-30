name: Update Contributors List

on:
  push:
    branches:
      - main

jobs:
  update-contributors:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Generate CONTRIBUTORS.md
        run: |
          git shortlog -s -n > CONTRIBUTORS.md
          sed -i 's/^/    /' CONTRIBUTORS.md

      - name: Commit and push changes
        run: |
          git config --global user.name 'github-actions'
          git config --global user.email 'actions@github.com'
          git add CONTRIBUTORS.md
          git commit -m 'Update contributors list'
          git push
