name: Daily Key Rotate

on:
  schedule:
    - cron: '0 0 * * *' # Todo dia 00:00 UTC
  workflow_dispatch: {} # Permite rodar manualmente

permissions:
  contents: write

jobs:
  generate-and-commit:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo
        uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Generate key
        run: node scripts/generate-key.js > key.txt

      - name: Commit key.txt
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "github-actions[bot]@users.noreply.github.com"
          git add key.txt
          if git diff --cached --quiet; then
            echo "No changes to commit"
          else
            git commit -m "Update key: $(date -u +'%Y-%m-%d')"
            git push
          fi
