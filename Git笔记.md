

### git diff --staged

git diff --staged   表示这个命令会显示已暂存的更改，即你使用 `git add` 命令添加到暂存区的更改。

### git diff 

git diff    表示要查看未暂存的更改，即工作区中已经修改但尚未添加到暂存区的更改

**`git difftool`：**

- **比较工作区和暂存区（未暂存的更改）：** 默认情况下，`git difftool` 比较的是工作区（当前的修改）和暂存区（使用 `git add` 准备提交的更改）之间的差异。
- **用途：** 用于查看尚未添加到暂存区的更改，或者查看已暂存的更改与工作区的不同。

**`git difftool --staged`：**

- **比较暂存区和上一次提交（已暂存的更改）：** `git difftool --staged` 比较的是暂存区（已通过 `git add` 准备提交的更改）和上一次提交的快照之间的差异。

- **用途：** 用于查看即将被提交的更改，或者查看已经被暂存但还未提交的更改与上一次提交的不同。

  

  总结来说，`git difftool` 用于比较工作区和暂存区，而 `git difftool --staged` 用于比较暂存区和上一次提交

## 在工作区中被修改但尚未提交的文件还原到它们在最后一次提交时的状态。

`git restore *` 

### git restore  (文件)    意味着你在工作目录中做了一些更改，但是还没有提交到版本控制。这种情况下，如果你希望撤销这些更改并还原文件到最后一次提交的状态    

git restore --staged file1.js       这行命令是表示 撤销在暂存区中file1.js中的修改全部放到工作区中

#### `git restore *` 命令表示撤销所有已修改的但尚未暂存（即还没有通过 `git add` 添加到暂存区）的文件的更改。这个命令将会将所有在工作区中被修改但尚未提交的文件还原到它们在最后一次提交时的状态。



## git clean -fd

#### 先用 git restore . 撤销所有文件  但有一个问题，在修改时我们添加了一个新文件,但是最后一次提交中没有这个文件我们就想要用下面的命令来删除这个文件



## 如果有一个文件我们不小心删除了我们怎么恢复它

如果有一个文件我们不小心删除了我们怎么恢复它

git log --oneline toc.txt  查看是否被删除

git log --oneline -- toc.txt 来查看所有接触这个文件的提交内容

`git checkout a642e12 toc.txt` 是一个Git命令，它的作用是从特定的提交（在这里是 `a642e12`）中恢复（或者说检出）`toc.txt` 文件的版本

再通过 git commit -m "Restore toc.txt" 来恢复这个文件

## 追责

`git blame audience.txt`    这个命令可以帮助你了解文件的修改历史，以及每一行内容的修改者。

##  设置版本v1.0...

git tag v1.0 50db987    这个表示在这个提交中(50db987) 我们把它标签设置成v1.0 

git ckeckout v1.0

`git tag -n` 是一个Git命令，用于显示所有标签（tags）的列表，并附带每个标签的附注信息（annotation）。这个命令的输出会列出所有标签的名称和对应的附注信息，方便你查看每个标签的相关信息。

git tag -d v1.1     表示删除v1.1标签

## 切换到特定提交

`git checkout v1.0` 的命令用途是将你的工作目录和暂存区切换到标签 `v1.0` 所指向的特定提交状态。标签通常用于标记项目的特定版本，比如软件的发布版本。当你切换到一个特定的标签时，你可以：

1. **查看特定版本的代码：** 切换到标签后，你会处于该标签所指向的提交状态，可以查看这个特定版本的代码。
2. **修复特定版本的问题：** 如果在标签 `v1.0` 的版本中发现了问题，你可以切换到这个标签，然后在这个基础上进行修复。
3. **创建新的分支：** 你可以在标签上创建一个新的分支，用于开发新功能或修复问题，而不会影响到已发布的版本。
4. **进行测试：** 你可以在特定版本上进行测试，确保这个版本的功能正常运行。

切换到标签并不会影响到其他分支的状态，它只会改变你当前所在的位置。当你想回到其他分支的开发时，可以使用 `git checkout` 命令再次切换到其他分支。

请注意，在切换到标签时，你的工作目录中不能有未提交的更改，因为这样会导致切换失败。你需要确保在切换之前提交你的更改或者将它们保存到暂存区。

# 分支

### 查看分支

git branch   表示查看分支

### 添加分支

git branch bugfix   表示添加一个bugfix 分支

### 跳转分支

git switch bugfix     表示跳到bugfix分支上

`git branch -m bugfix bugfix/signup-form`    表示用于将分支名从 `bugfix` 修改为 `bugfix/signup-form`

### 删除分支

git branch -d bugfix/signup-form    表示删除 bugfix/signup-form 分支  把-d改为-D表示为强制删除

git log master..bugfix/signup-form  表示  给我看看在bugfix/signup-form分支的所以提交



### 31.我们在工作目录中或者在暂存区修改了一些东西，但是我们还不想提交，而且我们又要到其他分支中去 ，这个时候就需要把它们放到一个储存空间中

`git stash push -m "NEW tax rules"` 是一个Git命令，用于将当前工作目录中的所有未提交的更改（包括暂存区和工作目录的更改）暂存（stash）起来，并添加一条附带消息 "NEW tax rules" 的描述。

如果还要添加一个文件到储存空间中我们就需要添加一个-a 

例如  git stash push -am "My old stach"

git stash list  显示当前仓库中所有的stash

**`git stash apply`：** 将最新的stash中的更改提出到工作目录中，但不删除stash。

git stash show stash@{1}   在Git中，`git stash show` 命令用于显示stash中的更改。`stash@{n}` 表示第 `n` 个stash，其中 `n` 是stash的索引号。索引号是从0开始的，表示最新的stash为 `stash@{0}`，之前的stash依次为 `stash@{1}`, `stash@{2}`, 以此类推。

git stash drop 1  删除第一个索引的储存文件

`git stash clear` 是一个Git命令，用于清空（删除）当前仓库中所有的stash。





### 合并分支

git merge bugfix/signup-form          在master主分支上把bugfix/signup-form合并

git merge --no-ff bugfix/loging-form      通过使用 `--no-ff` 标志，你告诉Git，不管是否存在快进合并的可能性，都要创建一个新的合并提交，以保留分支的独立性和合并历史



### 创建这个分支并跳转到这个分支

git switch -C feature/change-password  表示创建这个分支并跳转到这个分支



### 取消合并

当有合并冲突时，我们现在不行需要立马搞这个合并冲突可以使用`git merge --abort`来返回之前的状态



### 撤回合并

`git reset --hard HEAD~1` 这个命令的效果是将当前分支的 HEAD 指针和工作目录都设置为当前提交的父提交，也就是回退到上一个提交的状态。

`git reset --hard 3adc826` 命令的含义是将当前分支（通常是你所在的分支）的 HEAD 指针和工作目录都强制移动到指定的提交（在这个例子中是 `3adc826`）。这个操作会丢弃掉当前提交及其之后的所有提交，也就是将分支历史重置到指定的提交状态。

git revert -m 1 HEAD   撤最新的提交，返回一个新的提交为父类最新的提交前面的一个提交



### 压缩分支提交

`git merge --squash bugfix/photo-upload`   命令的作用是将 `bugfix/photo-upload` 分支的所有提交整合成一个新的提交，并将这个新的提交合并到当前分支。这样，多个小的提交会被“压缩”成一个单一的提交。在使用 `git merge --squash` 命令时，合并的分支（比如 `bugfix/photo-upload` 分支）的所有提交会被整理为一个新的提交，并且这些修改会被放入主分支（当前分支）的暂存区，而不是直接提交到主分支。因此，在执行 `git merge --squash bugfix/photo-upload` 后，修改会在主分支的暂存区等待你手动进行一次提交，这个提交将包含了 `bugfix/photo-upload` 分支的所有修改。



### 在不合并整个分支的情况下，将特定的提交引入到你当前的分支中。

`cherry-picking` 是 Git 中的一个操作，用于选择某一个分支上的单个提交，并将它应用到另一个分支上。这个操作允许你在不合并整个分支的情况下，将特定的提交引入到你当前的分支中。

**如何使用 Cherry-Pick：**

1. **确定目标提交：** 首先，确定你想要从其他分支上引入的特定提交的哈希值（SHA-1 标识）。

2. **切换到目标分支：** 在你想要引入这个提交的分支上执行 `git checkout branch-name`，将分支切换到你希望引入提交的目标分支上。

3. **执行 Cherry-Pick：** 使用以下命令执行 Cherry-Pick 操作，将目标提交应用到当前分支：

   ```
   bashCopy code
   git cherry-pick <commit-hash>
   ```

   这里 `<commit-hash>` 是你希望引入的提交的哈希值。

4. **处理冲突（如果有的话）：** 如果在 Cherry-Pick 操作中出现了冲突，你需要手动解决这些冲突，使用 `git add` 标记为已解决，然后执行 `git cherry-pick --continue` 继续 Cherry-Pick 过程。

5. **完成 Cherry-Pick：** 当没有冲突或者冲突都被解决后，Cherry-Pick 操作就完成了，目标提交已经被引入到当前分支中。

Cherry-Pick 操作通常用于从其他分支上选择性地引入某个修复、特性或者提交，而不是整个分支的合并。

39.

另外一种方式如何从另一个分支中挑出一个特定的提交，并将其应用于当前分支

git restore --source=feature/send-email -- toc.txt  这个命令的作用是，将 `feature/send-email` 分支上的 `toc.txt` 文件的内容恢复到当前分支中的同一文件中。这会覆盖当前分支上的 `toc.txt` 文件，将其内容替换为 `feature/send-email` 分支上的版本。

这些文件就会到暂存区，需要把他们提交





# 协作

### 远程追踪分支

```bash
git branch -u origin/{branch}
```

### 拉取

拉取远程仓库的最新提交，本地什么都没改变。

```bash
git fetch
```

拉取特定分支的提交

```
git fetch origin branch {哈希值}
```

### 拉取并合并

pull = fetch + merge 

```bash
git pull
```



```
git pull -rebase
```

`git pull --rebase` 命令是 Git 中用来更新本地分支的一个变体，它结合了 `git pull` 和 `git rebase` 的功能。它的作用是从远程仓库拉取最新的更改，并将这些更改应用到你的本地提交之上。

#### 工作原理

通常，`git pull` 会执行两步操作：

1. `git fetch`：从远程仓库获取最新的提交。
2. `git merge`：将这些提交合并到当前分支。

而 `git pull --rebase` 则将 `merge` 步骤替换为 `rebase`，其工作流程如下：

1. `git fetch`：从远程仓库获取最新的提交。
2. `git rebase`：将本地提交在远程提交之上重新应用。

#### 例子

假设你有如下提交历史：

```
mathematica复制代码A - B - C (origin/master)
     \
      D - E (master)
```

如果你执行 `git pull --rebase`，它会进行如下操作：

1. `git fetch` 拉取最新的提交 `A - B - C`。
2. `git rebase`：将本地的 `D` 和 `E` 重新应用到 `C` 之后。

结果如下：

```
mathematica
复制代码
A - B - C - D' - E' (master)
```

其中，`D'` 和 `E'` 是重新应用的提交，具有新的提交哈希。

#### 为什么使用 `--rebase`

使用 `--rebase` 的主要好处是可以保持提交历史的线性结构，避免合并提交（merge commit）的混乱。这使得提交历史更加清晰，尤其是在与多个开发者协作时。



### 推送

```bash
git push
```

`git push` 命令用于将本地的提交推送到远程仓库。它的基本语法是：

```bash
git push <remote> <branch>
```

例如：

```bash
git push origin master
```

这将本地 `master` 分支的提交推送到远程仓库 `origin` 上的 `master` 分支。

#### 可以 `push` 的情况

1. **无冲突的提交**：如果你的本地分支包含的提交是远程分支的延续（即没有其他人在远程仓库中修改过你本地没有的提交），你可以顺利推送。

   ```bash
   git push origin master
   ```

2. **推送新分支**：如果你创建了一个新的分支，并且该分支在远程仓库中还不存在，可以直接推送。

   ```bash
   git push origin new-branch
   ```

3. **快进合并**：你的提交可以直接应用在远程分支的当前提交之后，即远程分支可以通过“快进”方式合并你的提交。

4. **强制推送**：使用 `--force` 选项强制推送本地分支到远程，即使会覆盖远程的提交历史。这通常用于推送 rebase 后的更改。

   ```bash
   git push --force origin master
   ```

#### `push` 被拒绝的情况

1. **非快进更新被拒绝**：如果远程分支包含你本地没有的提交，推送会被拒绝，因为这会导致提交历史分叉。你需要先拉取这些更改并解决冲突，然后才能推送。

   ```bash
   git pull origin master --rebase
   git push origin master
   ```

2. **权限问题**：你对远程仓库没有写权限。此时，你需要联系仓库管理员来获得权限。

3. **分支保护**：远程仓库可能对某些分支（如 `master` 或 `main`）启用了保护，禁止直接推送。你需要通过 Pull Request 来进行更改。

4. **推送冲突**：在你开始推送之前，另一个开发者推送了新提交。你需要拉取他们的更改，解决冲突后再推送。

5. **本地分支落后太多**：如果你本地分支与远程分支的差异太大，推送可能会被拒绝。此时需要通过 `git pull` 获取远程最新更改。

#### 处理被拒绝的推送

1. **获取远程更新**：首先拉取远程分支的最新更新。

   ```bash
   git pull origin master --rebase
   ```

2. **解决冲突**：如果在拉取过程中遇到冲突，解决这些冲突并提交。

3. **重新推送**：解决冲突后再次推送。

   ```bash
   git push origin master
   ```

4. **使用强制推送（慎用）**：如果确定需要覆盖远程分支的提交历史，可以使用 `--force` 选项。

   ```bash
   git push --force origin master
   ```

强制推送可能会导致其他开发者的工作丢失，使用时要非常谨慎，通常需要团队协作的沟通和确认。

### 远程仓库设置分支

```
git push -u origin feature/change-password
```

执行 `git push -u origin feature/change-password` 这个命令后，会发生以下几件事情：

1. 如果远程仓库 `origin` 中不存在名为 `feature/change-password` 的分支，Git 会将本地的 `feature/change-password` 分支推送到远程仓库，并在远程仓库上创建这个分支。
2. `-u` 参数（或 `--set-upstream`）会将本地的 `feature/change-password` 分支与远程仓库的 `origin/feature/change-password` 分支关联起来。这意味着以后在该分支上执行 `git push` 或 `git pull` 时，Git 将自动识别并推送或拉取到 `origin/feature/change-password` 分支。

#### 完整操作流程

1. **创建并切换到新分支**：

   首先，你可能会创建一个新的功能分支并切换到该分支上。

   ```bash
   git checkout -b feature/change-password
   ```

   这将创建并切换到名为 `feature/change-password` 的新分支。

2. **进行修改并提交**：

   在这个新分支上，你会进行代码修改并提交。

   ```bash
   git add .
   git commit -m "Implement change password feature"
   ```

3. **推送分支并设置上游分支**：

   接下来，使用 `git push -u origin feature/change-password` 将分支推送到远程仓库。

   ```bash
   git push -u origin feature/change-password
   ```

#### 结果

执行 `git push -u origin feature/change-password` 后，会发生以下情况：

1. **推送分支**：本地的 `feature/change-password` 分支被推送到远程仓库 `origin` 中，远程仓库中会创建一个名为 `feature/change-password` 的新分支。
2. **设置上游分支**：本地的 `feature/change-password` 分支将被配置为跟踪 `origin/feature/change-password`。这意味着以后你可以使用简化命令进行推送和拉取操作。

例如，以后你可以直接使用 `git pull` 和 `git

push` 而不需要指定远程和分支名称：

```bash
# 拉取最新的更改
git pull

# 推送新的更改
git push
```

这些命令将自动应用到当前的 `feature/change-password` 分支，因为它已经设置了上游分支 `origin/feature/change-password`。

#### 总结

`git push -u origin feature/change-password` 是一个非常有用的命令，特别是在多人协作开发时，能够简化和规范推送和拉取操作，确保本地和远程分支的一致性。



### 正常协助工作流程（分支）

首先在GitHub上创建一个远程分支feature/change-password

1. `git switch -C feature/change-password`：
   - 这个命令创建了一个名为 `feature/change-password` 的新分支，并且立即切换到这个新创建的分支上。如果这个分支在远程仓库中已经存在，Git会让你知道它已经存在，不过它会在本地仓库中创建一个分支并切换到该分支上。

2. `origin/feature/change-password`：
   - 这个部分指定了分支的起点，即从远程仓库中的 `feature/change-password` 分支进行跟踪和拉取。通常，`origin/feature/change-password` 表示远程仓库中的分支，而 `feature/change-password` 表示本地仓库中的分支。

综合起来，这两个命令一起做了以下几件事情：

- `git switch -C feature/change-password` 创建了一个本地分支 `feature/change-password` 并立即切换到该分支。
- `origin/feature/change-password` 指示了该分支的起点，表示你希望该分支与远程仓库中的 `feature/change-password` 分支进行关联。

因此，这些命令的组合效果是在本地和远程仓库中都创建一个新分支 `feature/change-password`，并将本地分支设置为跟踪远程分支，以便后续的推送和拉取操作。

#### 步骤

1.创建一个远程分支feature/change-password

2.程序员拉取，这个远程分支跟踪这个分支

3.在这个feature/change分支上工作

4.当工作完成后想要合并到主分支上，先在本地跳转到主分支，合并feature/change分支，

5.然后git push把远程分支都放到最新提交上，

6.当需要合并时，需要Pull Request和队友进行讨论，审查，再进行合并

#### 删除远程仓库分支

```
git push -d origin feature/cjange-password
```

#### 删除本地分支

```
git branch -d feature/change-password
```

#### 删除本地远程分支

`git remote prune origin` 是一个用于清理本地远程跟踪分支的命令。它的作用是删除本地仓库中那些远程仓库已经删除的分支的引用。这些已经删除的分支可能由于其他开发者在远程仓库中执行了删除操作，而本地仓库中的远程跟踪分支没有及时同步删除。

具体来说，当你从远程仓库拉取了分支并创建了本地远程跟踪分支（例如 `origin/feature-branch`），如果后来远程仓库中删除了这个分支，但本地仓库中的远程跟踪分支依然存在，这时就可以使用 `git remote prune origin` 来清理这些本地已经过时的远程跟踪分支。



# 修改历史

## 删除提交

#### 如果你想撤回最新一次提交并将改动放到工作区，可以使用 `git reset` 命令。具体来说，`git reset --soft HEAD~1` 会将最新一次提交的改动撤回并放到暂存区，而 `git reset --mixed HEAD~1` 会将这些改动放到工作区。

#### git reset --hard HEAD~1当你想完全撤销最后一次提交的所有改动，并且丢弃工作区和暂存区的所有改动时使用。

`git reset` 命令有不同的选项（`--soft`、`--mixed` 和 `--hard`），用于指定如何处理当前分支、暂存区和工作区的状态。以下是详细解释：

### 1. `git reset --soft HEAD~1`

- **操作说明**：将当前分支的 HEAD 移动到上一个提交（`HEAD~1`），但是保留暂存区和工作区的改动。
- **效果**：
  - HEAD 指针移动到上一个提交。
  - 暂存区（staging area）保留改动。
  - 工作区（working directory）保留改动。
- **用例**：当你想撤销最后一次提交但保留改动，准备重新提交时使用。

```bash
git reset --soft HEAD~1
```

#### 示例

假设提交历史如下：

```plaintext
* commit C (HEAD)
* commit B
* commit A
```

执行 `git reset --soft HEAD~1` 后，提交历史变为：

```plaintext
* commit B (HEAD)
* commit A
```

但是，commit C 的改动仍在暂存区和工作区。

### 2. `git reset --mixed HEAD~1`（或 `git reset HEAD~1`）

- **操作说明**：将当前分支的 HEAD 移动到上一个提交（`HEAD~1`），保留工作区的改动，但清空暂存区的改动。这是 `git reset` 的默认行为。
- **效果**：
  - HEAD 指针移动到上一个提交。
  - 暂存区（staging area）清空改动。
  - 工作区（working directory）保留改动。
- **用例**：当你想撤销最后一次提交并且将改动退回到工作区，准备进一步修改时使用。

```bash
git reset --mixed HEAD~1
# 或者简写为
git reset HEAD~1
```

#### 示例

假设提交历史如下：

```plaintext
* commit C (HEAD)
* commit B
* commit A
```

执行 `git reset --mixed HEAD~1` 或 `git reset HEAD~1` 后，提交历史变为：

```plaintext
* commit B (HEAD)
* commit A
```

commit C 的改动从暂存区移除，但保留在工作区。

### 3. `git reset --hard HEAD~1`

- **操作说明**：将当前分支的 HEAD 移动到上一个提交（`HEAD~1`），并且清空暂存区和工作区的改动。
- **效果**：
  - HEAD 指针移动到上一个提交。
  - 暂存区（staging area）清空改动。
  - 工作区（working directory）清空改动。
- **用例**：当你想完全撤销最后一次提交的所有改动，并且丢弃工作区和暂存区的所有改动时使用。

```bash
git reset --hard HEAD~1
```

#### 示例

假设提交历史如下：

```plaintext
* commit C (HEAD)
* commit B
* commit A
```

执行 `git reset --hard HEAD~1` 后，提交历史变为：

```plaintext
* commit B (HEAD)
* commit A
```

commit C 的改动完全被移除，包括暂存区和工作区。

### 总结

- `git reset --soft HEAD~1`：HEAD 移动到上一个提交，暂存区和工作区的改动保留。适用于撤销最后一次提交并准备重新提交。
- `git reset --mixed HEAD~1` 或 `git reset HEAD~1`：HEAD 移动到上一个提交，工作区的改动保留，暂存区的改动清空。适用于撤销最后一次提交并将改动退回到工作区进行修改。
- `git reset --hard HEAD~1`：HEAD 移动到上一个提交，暂存区和工作区的改动全部清空。适用于完全撤销最后一次提交及其改动。

根据你的需求选择合适的 `reset` 选项，以确保正确管理提交和改动。

## 恢复丢失的commit

如果你已经使用 `git reset --soft HEAD~1` 并且想恢复那个丢失的提交，可以通过 Git 的 `reflog` 功能来找到并恢复那个提交。`reflog` 记录了所有的 HEAD 改变，可以帮助你找回丢失的提交。

### 步骤

1. **查看 reflog**：
   - 使用 `git reflog` 命令查看最近的 HEAD 操作记录。这个命令会列出最近的 HEAD 移动，包括提交、重置、合并等操作。

2. **找到丢失的提交**：
   - 在 reflog 输出中找到你丢失的提交的哈希值（通常是一个 7-40 位的 SHA-1 哈希）。

3. **恢复丢失的提交**：
   - 使用 `git reset --soft <commit-hash>` 或 `git checkout <commit-hash>` 恢复到那个提交。

### 详细步骤

#### 1. 查看 reflog

```bash
git reflog
```

输出可能类似于：

```plaintext
abc1234 HEAD@{0}: reset: moving to HEAD~1
def5678 HEAD@{1}: commit: Added new feature
...
```

在这个例子中，`def5678` 就是你丢失的提交的哈希值。

#### 2. 恢复丢失的提交

有几种方法可以恢复丢失的提交：

##### 方法 1：软重置到丢失的提交

如果你想保留当前的工作目录和暂存区状态，并把 HEAD 移动到丢失的提交：

```bash
git reset --soft def5678
```

##### 方法 2：检查丢失的提交

如果你想临时查看那个丢失的提交，可以使用 `git checkout`：

```bash
git checkout def5678
```

注意：这会让你的 HEAD 处于“分离头指针”状态，此时你并未在任何分支上。

##### 方法 3：创建一个新的分支

如果你想在一个新的分支上恢复丢失的提交：

```bash
git checkout -b recover-branch def5678
```

这样会创建一个名为 `recover-branch` 的新分支，并将它指向丢失的提交。

#### 3. 确认恢复

无论你使用哪种方法，恢复提交后，都可以使用 `git log` 确认提交已经恢复：

```bash
git log
```

### 总结

通过 `git reflog`，你可以找到并恢复因 `git reset` 操作而丢失的提交。`reflog` 记录了所有 HEAD 的移动，是恢复误操作的重要工具。



## 压缩提交

Squash
