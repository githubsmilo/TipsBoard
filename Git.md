#### [Reset local repository branch to be just like remote repository HEAD](http://stackoverflow.com/questions/1628088/reset-local-repository-branch-to-be-just-like-remote-repository-head)
1. `$ git fetch origin`
2. `$ git reset --hard origin/master`

#### [Reset latest commit on git local repository](http://stackoverflow.com/questions/927358/undo-last-git-commit)
1. `$ git reset --soft HEAD^`

#### [Show git branch on terminal](http://blog.tinucleatus.com/?p=275)
1. .bashrc 혹은 .bash_profile에 아래 정보 추가
2. ``export PS1="\[\033[00m\]\u@\h\[\033[00m\]:\[\033[00m\]\w\[\033[00m\] \`ruby -e \"print (%x{git branch 2> /dev/null}.split(%r{\n}).grep(/^\*/).first || '').gsub(/^\* (.+)$/, '(\1) ')\"\`\[\033[00m\]$\[\033[00m\] "``

#### [Show git tree on terminal](http://stackoverflow.com/questions/1064361/unable-to-show-a-git-tree-in-terminal)
1. `$ git config --global alias.tree "log --graph --decorate --pretty=oneline --abbrev-commit --all"`
2. `$ git tree`

#### [How to export git repository](http://stackoverflow.com/questions/160608/how-to-do-a-git-export-like-svn-export)
1. `$ git archive master | tar -x -C /somewhere/else`
2. `$ git archive master | bzip2 >source-tree.tar.bz2`
3. `$ git archive --format zip --output /full/path/to/zipfile.zip master`

#### How to migrate from subversion to git
1. git 유저를 생성
2. git 정보가 저장될 repository 디렉토리 생성
  1. `$ mkdir /data/git`

3. 서버측에 저장할 프로젝트를 subversion으로부터 가져옴 (revision 1000까지)
  1. `$ cd ~/`
  2. `$ git svn clone svn://path GIT_DIR -r1:1000`

4. public repository를 만들기 위한 설정
  1. `$ cd ~/`
  2. `$ git clone --bare GIT_DIR`
  3. `$ touch GIT_DIR.git/git-daemon-export-ok`

5. GIT_DIR.git를 git repository로 이동
  1. `$ sudo -u git cp -R GIT_DIR.git /data/git/GIT_DIR`
  2. `$ cd /data/git/GIT_DIR`
  3. `$ sudo git --bare update-server-info`
  4. `$ sudo mv hooks/post-update.sample hooks/post-update`

6. 다른 컴퓨터에서 clone 명령을 수행하여 파일을 제대로 받아오는지 확인
  1. `$ git clone git@192.168.1.1:/data/git/GIT_DIR DIR_NAME`

7. Git 개인 설정
