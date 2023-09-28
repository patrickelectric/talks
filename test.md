---
author: Patrick
---

# Git Otimizado, Truques e Ferramentas Essenciais

 -   Patrick José Pereira
 -   [patrickelectric](https://github.com/patrickelectric)
 - 󰌻  [patrickelectric](https://linkedin.com/in/patrickelectric)
 -   patrickelectric@gmail.com
---

## Por que essa apresentação existe ?

 - Melhorar fluxo de trabalho
 - Histórico mais limpo e útil
 - Agilidade em resolver problemas
 - Ter uma experiência mais agradável com Git

---

# Commands

---

# Commands
  1. git (add / checkout / stash)

---

# Commands
  1. git (add / checkout / stash)
  2. git (add / checkout / stash) --patch

---

# Commands
  1. git (add / checkout / stash)
  2. git (add / checkout / stash) --patch
  3. git stash

---

# Commands
  1. git (add / checkout / stash)
  2. git (add / checkout / stash) --patch
  3. git stash
  4. git rebase

---

# Commands
  1. git (add / checkout / stash)
  2. git (add / checkout / stash) --patch
  3. git stash
  4. git rebase
  5. git rebase --interactive --autostash (--autosquash)

---

# Commands
  1. git (add / checkout / stash)
  2. git (add / checkout / stash) --patch
  3. git stash
  4. git rebase
  5. git rebase --interactive --autostash (--autosquash)
  6. cherry-pick

---

## $ git add

---

## $ git add

Our working tree

```
   o Untracked changes
   o Unstaged changes
   o [master] frontend: package: Use latest version of vite
   o frontend: package: Remove vitejs/plugin-vue
   o ...
```

---

## $ git add

git add bun.lockb

```
   o Untracked changes
   o Unstaged changes
 󰁔 o Staged changes
   o [master] frontend: package: Use latest version of vite
   o frontend: package: Remove vitejs/plugin-vue
   o ...
```

---

## $ git add

git commit -sm "frontend: Update bun.lockb"

```
   o Untracked changes
   o Unstaged changes
 󰁔 o [master] frontend: Update bun.lockb
   o frontend: package: Use latest version of vite
   o frontend: package: Remove vitejs/plugin-vue
   o ...
```
---

## $ git add

Our working tree

```
   o Untracked changes
   o Unstaged changes
   o [master] frontend: package: Use latest version of vite
   o frontend: package: Remove vitejs/plugin-vue
   o ...
```

---

## $ git checkout

---

## $ git checkout

Our working tree

```
   o Untracked changes
   o Unstaged changes
   o [master] frontend: package: Use latest version of vite
   o frontend: package: Remove vitejs/plugin-vue
   o ...
```
---

## $ git checkout

git checkout bun.lockb

```
   o Untracked changes
   o [master] frontend: package: Use latest version of vite
   o frontend: package: Remove vitejs/plugin-vue
   o ...
```
---

## $ git checkout

Our working tree

```md
   o [*master*] core: frontend: package: Use latest version of vite
   o core: frontend: package: Remove vitejs/plugin-vue
   │ o [move-static-assets] core: frontend: vite.config: Remove ...
   │ o core: frontend: Move some assets to be compiled with source ...
   │ │ o [size_extension] core: frontend: components: kraken: ...
   │ │ o core: services: kraken: setup: Add psutil library
   o─┴─┘ README: Update badges link
   o ...
```

---

## $ git checkout

git checkout move-static-assets

```md
   o [*move-static-assets*] core: frontend: vite.config: Remove ...
   o core: frontend: Move some assets to be compiled with source ...
   │ o [master] core: frontend: package: Use latest version of vite
   │ o core: frontend: package: Remove vitejs/plugin-vue
   │ │ o [size_extension] core: frontend: components: kraken: ...
   │ │ o core: services: kraken: setup: Add psutil library
   o─┴─┘ README: Update badges link
   o ...
```

---

## $ git checkout

Our working tree

```
   o [*master*] frontend: package: Use latest version of vite
   o frontend: package: Remove vitejs/plugin-vue
   o README: Update badges link
   o ...
```

---

## $ git checkout

git checkout -b new-feature

```
   o [*new-feature*][master] frontend: package: Use latest version of vite
   o frontend: package: Remove vitejs/plugin-vue
   o README: Update badges link
   o ...
```

---

## $ git checkout

git commit -sm "This is an important message"

```
   o [*new-feature*] This is an important message
   o [master] frontend: package: Use latest version of vite
   o frontend: package: Remove vitejs/plugin-vue
   o README: Update badges link
   o ...
```

---

## $ git checkout

git checkout -

```
   o [new-feature] This is an important message
   o [*master*] frontend: package: Use latest version of vite
   o frontend: package: Remove vitejs/plugin-vue
   o README: Update badges link
   o ...
```

---

## --patch

---

## --patch

- git add --patch
- git checkout --patch
- git stash --patch

---
## --patch

git add --patch

```diff
diff --git a/src/runner.rs b/src/runner.rs
index e85c103..59978fb 100644
--- a/src/runner.rs
+++ b/src/runner.rs
@@ -141,7 +141,7 @@ impl PipelineRunner {

   match msg.view() {
     MessageView::Eos(eos) => {
-      warn!("Received EndOfStream: {eos:#?}");
+      debug!("Received EndOfStream: {eos:?}");
       pipeline.debug_to_dot_file_with_ts(
         gst::DebugGraphDetails::all(),
         format!("pipeline-{pipeline_id}-eos"),
(1/1) Stage this hunk [y,n,q,a,d,e,?]?
```

---

## --patch

git checkout --patch

```diff
diff --git a/src/runner.rs b/src/runner.rs
index e85c103..59978fb 100644
--- a/src/runner.rs
+++ b/src/runner.rs
@@ -141,7 +141,7 @@ impl PipelineRunner {

   match msg.view() {
     MessageView::Eos(eos) => {
-      warn!("Received EndOfStream: {eos:#?}");
+      debug!("Received EndOfStream: {eos:?}");
       pipeline.debug_to_dot_file_with_ts(
         gst::DebugGraphDetails::all(),
         format!("pipeline-{pipeline_id}-eos"),
(1/1) Discard this hunk from worktree [y,n,q,a,d,e,?]?
```

---

## --patch

git stash --patch

```diff
diff --git a/src/runner.rs b/src/runner.rs
index e85c103..59978fb 100644
--- a/src/runner.rs
+++ b/src/runner.rs
@@ -141,7 +141,7 @@ impl PipelineRunner {

   match msg.view() {
     MessageView::Eos(eos) => {
-      warn!("Received EndOfStream: {eos:#?}");
+      debug!("Received EndOfStream: {eos:?}");
       pipeline.debug_to_dot_file_with_ts(
         gst::DebugGraphDetails::all(),
         format!("pipeline-{pipeline_id}-eos"),
(1/1) Stash this hunk [y,n,q,a,d,e,?]?
```

---

## stash

---

## stash

- git stash
- git stash --patch
- git stash --include-untracked

---

## stash

- git stash
- git stash --patch
- git stash --include-untracked

> Affects both **staged** and **unstaged** area

---

## stash

git stash --list

---

## stash

git stash --list

```
stash@{1}: WIP on update-libs: d8678035 core: frontend: Update bun.lockb
stash@{2}: WIP on master: d4a43b59 core: frontend: vite.config: Remove public alias
stash@{3}: WIP on master: d4a43b59 core: frontend: vite.config: Remove public alias
stash@{4}: WIP on master: eea05f58 core: frontend: gitignore: Add components.d.ts
```
---

## stash

git stash show stash@\{1\} --patch

```diff
diff --git a/core/frontend/vite.config.js b/core/frontend/vite.config.js
index 7dcbf58b..8cdec8b1 100644
--- a/core/frontend/vite.config.js
+++ b/core/frontend/vite.config.js
@@ -123,11 +123,13 @@ export default defineConfig({
         target: SERVER_ADDRESS,
         changeOrigin: true,
         ws: true,
+        secure: false,
       },
       '^/mavlink2rest': {
         target: SERVER_ADDRESS,
         changeOrigin: true,
         ws: true,
+        secure: false,
       },
       '^/mavlink-camera-manager': {
         target: SERVER_ADDRESS,
```
---

## stash

git stash apply stash@\{1\}

---

# Danger zone

---

# Danger zone

- git clean
- git reset --hard
- git rm FILE

---

# Danger zone

- git clean # git stash --include-untracked
- git reset --hard # git stash
- git rm FILE # git stash push FILE --include-untracked

---


# Git Configuration

```bash
git config --edit --global
```

~/.gitconfig

---

# Git Alias
```toml
[alias]
```
---

# Git Alias
```toml
[alias]
  # I have problems
  ck = checkout
```

Exemplo:
```bash
git ck new-feature
```

---

# Git Alias
```toml
[alias]
  # Check biggest contributors
  score = shortlog -n --all --no-merges
```

---

# Git Alias
```toml
[alias]
  branch-by-age = for-each-ref --sort=committerdate refs/heads/ --format='%(authordate) \t %(refname:short)'
```

---

# Git Alias
```toml
[alias]
  fix-old = "!f() { git commit --fixup=$(git rev-parse HEAD~$(($1-1))); }; f"
```

---

# Git Alias
```toml
[alias]
  stats = "!f() { \
    status=$(git status --porcelain); \
    IFS=$'\\n'; \
    for line in $status; do \
      file=${line:3}; \
      case ${line:0:2} in \
      \" M\") \
        echo -e \"\\e[31m󱠡 $file\\e[0m\" \
        ;; \
      \"M \") \
        echo -e \"\\e[32m $file\\e[0m\" \
        ;; \
      \"??\") \
        echo -e \"\\e[33m󱁏 $file\\e[0m\" \
        ;; \
      esac; \
    done; \
  }; f"
```

---

# Final tips

1. git commit --allow-empty -sm "First commit"

---
# Final tips

1. git commit --allow-empty -sm "First commit"
2. git commit --amend --no-edit

---
# Final tips

1. git commit --allow-empty -sm "First commit"
2. git commit --amend --no-edit
3. git reset HEAD~N

---
# Final tips

1. git commit --allow-empty -sm "First commit"
2. git commit --amend --no-edit
3. git reset HEAD~N
4. git stash apply stash@\{N\}

---
# Final tips

1. git commit --allow-empty -sm "First commit"
2. git commit --amend --no-edit
3. git reset HEAD~N
4. git stash apply stash@\{N\}
5. git reflog

---

# Thanks!

Questions ?

---

## Pre-process slides

You can add a code block with three tildes (`~`) and write a command to run *before* displaying
the slides, the text inside the code block will be passed as `stdin` to the command
and the code block will be replaced with the `stdout` of the command.

~~~graph-easy --as=boxart
[ A ] - to -> [ B ]
~~~

The above will be pre-processed to look like:

```
┌───┐  to   ┌───┐
│ A │ ────> │ B │
└───┘       └───┘
```
For security reasons, you must pass a file that has execution permissions
for the slides to be pre-processed. You can use `chmod` to add these permissions.

```bash
chmod +x file.md
```
