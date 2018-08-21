### 1撤销操作

#### 1.1提交后发现丢了几个文件没有提交或是想修改上一次提交说明（常用）

```javascript
/* 正常提交 */
git commit -m "发布v1.0"
/* 发现丢了修改记录，重新添加 */
git add changelog.md
/* 重新提交,仍以"发布v1.0的名义提交"，最终只有一个提交*/
/* 如果没有add，直接运行git commit --amend，就是修改上一次提交的说明 */
git commit --amend
```

#### 1.2撤销上一次的提交，但是保留暂存区和当前修改不变

```javascript
/* 正常提交 */
git commit -m "发布v1.0"
/* 将会撤销“发布v1.0”的提交，但是保留暂存区和当前目录中文件的修改 */
git reset --soft head~
```

#### 1.3撤销上一次的提交和暂存区修改，仅保留当前修改不变

```javascript
/* 正常提交 */
git commit -m "发布v1.0"
/* 将会撤销“发布v1.0”的提交和暂存区的修改，仅保留当前目录中文件的修改 */
git reset --mixed head~
```

#### 1.4撤销上一次的提交，并丢弃所有修改，包括暂存区和当前目录中的修改整体回到上上次的提交

```javascript
/* 正常提交 */
git commit -m "发布v1.0"
/* 将会撤销“发布v1.0”的提交，并丢弃所有的修改 */
git reset --hard head~
```

#### 1.5撤销暂存区和当前目录下所有文件的修改，整体回到上一次提交

注意：此操作非常危险，会丢失所有修改，直接整体回档到指定的版本，谨慎使用

```javascript
/* 正常提交 */
git commit -m "发布v1.0"
/* 修改多个文件 */
/* 添加到暂存区 */
git add .
/* 撤销暂存区和本地目录下所有文件的修改，并整体回档到上一次提交的状态 */
git reset --hard head
/* 可以修改HEAD为SHA-1值回档到任意版本 */
/* 使用git log查看每次提交的SHA-1值，可以仅指定前7位 */
git reset --hard 745d8cd
```

#### 1.6将文件提交到暂存区后撤销（常用）

在对文件执行git add操作后，重新撤回

```javascript
/* 添加文件到暂存区 */
git add README
/* 将文件从暂存区撤回 */
git reset HEAD READM
```

#### 1.7撤销对文件的修改

改后，发现思路不对，需要将文件恢复至原有状态

```javascript
/* 撤销对CHANGELOG.md文件的修改，请注意这是一个危险的命令，
 * 对指定文件的修改都会被取消，会还原成上次提交的样子 */
git checkout -- src/CHANGELOG.md
```

