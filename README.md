# Submodule Usage

#### Conception

- 將按照當時的 Submodule Head 紀錄再 Host Module 上。除非手動去 Update 否則 Submodule 會停留再那個 Commit HEAD。
- "git submodule foreach git pull origin" or "git submodule foreach --recursive git pull origin" 更進 Submodule 版本。
- git submodule status 查閱 Submodule 狀態。

```
git submodule add https://github.com/scott1028/git-study.git lib/git-study
git commit -am "add submodule"
git push origin
```

#### 從 Remote 抓 Code 下來

```
$ git clone http://localgitlab/test/git-study.git	← 此時 submodule 資料夾為空
$ git submodule init								← Prepare Submodule 資訊
$ git submodule update								← 抓下 submodule 檔案
```
