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

## Danger zone

- git clean # git stash --include-untracked
- git reset --hard # git stash
- git rm FILE # git stash push FILE --include-untracked


---

## rebase

---

## rebase

git rebase origin/master

---

## rebase

git rebase -i origin/master

---

## rebase

git rebase -i origin/master

```
pick 43013f99 store: autopilot: Add autopilot_type property
pick 0e70e64f components: health: HealthTrayMenu: Add autopilot type
pick 94f83cf5 views: Autopilot: Add autopilot type banner
pick 54bdc6d2 assets: Add banners
```

---

## rebase

git rebase -i origin/master

```
pick 0e70e64f components: health: HealthTrayMenu: Add autopilot type
pick 43013f99 store: autopilot: Add autopilot_type property
pick 94f83cf5 views: Autopilot: Add autopilot type banner
pick 54bdc6d2 assets: Add banners
```

---

## rebase

git rebase -i origin/master

```
pick 0e70e64f components: health: HealthTrayMenu: Add autopilot type
pick 43013f99 store: autopilot: Add autopilot_type property
pick 54bdc6d2 assets: Add banners
```

---

## rebase

git rebase -i origin/master

```
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase

```

---

## rebase

git rebase -i origin/master

```
pick a312c12e components: health: HealthTrayMenu: Fix autopilot type
pick 43013f99 store: autopilot: Add autopilot_type property
pick 0e70e64f components: health: HealthTrayMenu: Add autopilot type
pick 94f83cf5 views: Autopilot: Add autopilot type banner
pick 54bdc6d2 assets: Add banners
```

---

## rebase

git rebase -i origin/master

```
pick 43013f99 store: autopilot: Add autopilot_type property
pick a312c12e components: health: HealthTrayMenu: Fix autopilot type
pick 0e70e64f components: health: HealthTrayMenu: Add autopilot type
pick 94f83cf5 views: Autopilot: Add autopilot type banner
pick 54bdc6d2 assets: Add banners
```

---

## rebase

git rebase -i origin/master

```
pick 43013f99 store: autopilot: Add autopilot_type property
fixup a312c12e components: health: HealthTrayMenu: Fix autopilot type
pick 0e70e64f components: health: HealthTrayMenu: Add autopilot type
pick 94f83cf5 views: Autopilot: Add autopilot type banner
pick 54bdc6d2 assets: Add banners
```

---

## rebase

git rebase -i origin/master

```
pick 43013f99 store: autopilot: Add autopilot_type property
pick 7b8921ca components: health: HealthTrayMenu: Add autopilot type
pick 94f83cf5 views: Autopilot: Add autopilot type banner
pick 54bdc6d2 assets: Add banners
```

---

## rebase

---

## rebase

git commit --fixup 0e70e64f

---

## rebase

git commit --fixup 0e70e64f

```
a312c12e fixup! components: health: HealthTrayMenu: Add autopilot type
43013f99 store: autopilot: Add autopilot_type property
0e70e64f components: health: HealthTrayMenu: Add autopilot type
94f83cf5 views: Autopilot: Add autopilot type banner
54bdc6d2 assets: Add banners
```

---

## rebase

git rebase origin/master --autosquash

```
a312c12e fixup! components: health: HealthTrayMenu: Add autopilot type
43013f99 store: autopilot: Add autopilot_type property
0e70e64f components: health: HealthTrayMenu: Add autopilot type
94f83cf5 views: Autopilot: Add autopilot type banner
54bdc6d2 assets: Add banners
```

---

## rebase

git rebase origin/master --autosquash

```
43013f99 store: autopilot: Add autopilot_type property
0e70e64f components: health: HealthTrayMenu: Add autopilot type
94f83cf5 views: Autopilot: Add autopilot type banner
54bdc6d2 assets: Add banners
```

---

# Tools

---

# Tools

- [Tig (Text-mode Interface for Git)](https://github.com/jonas/tig)

---

# Tools

- [Tig (Text-mode Interface for Git)](https://github.com/jonas/tig)
- [Delta](https://github.com/dandavison/delta)

---

# Tools

- [Tig (Text-mode Interface for Git)](https://github.com/jonas/tig)
- [Delta](https://github.com/dandavison/delta)
- [Diff-so-fancy](https://github.com/so-fancy/diff-so-fancy)

---

# Tools

- [Tig (Text-mode Interface for Git)](https://github.com/jonas/tig)
- [Delta](https://github.com/dandavison/delta)
- [Diff-so-fancy](https://github.com/so-fancy/diff-so-fancy)
- [Absorb](https://github.com/tummychow/git-absorb)

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

- [Mastering Git - By Jakub Narębski](https://www.packtpub.com/product/mastering-git/9781783553754)
- [Pro Git - 280+ contributors](https://git-scm.com/book/en/v2)
---