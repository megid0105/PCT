cd ~/Desktop/Download/project/PCT

cat > HowTo-Run-Codex-Max.md << 'EOF'
# How to run Codex-Max for SAGE

## 1. Start from a clean tree
- In `SAGE_CORE_APP`:
  - `git status` must say "working tree clean".
  - `AGENTS.md`, `qc/`, and `codex-manifest.json` must exist.

## 2. Run Codex-Max with a requestId

```bash
cd ~/Desktop/Download/project/SAGE_CORE_APP
REQUEST_ID=$(uuidgen)

codex run << EOF
[REQUEST_ID: $REQUEST_ID]
...instructions...
EOF



then 

git status
git diff
git add ...
git commit -m "Codex-Max: <desc> [$REQUEST_ID]"
git push origin main
