# Лабораторный стенд с выполненным домашним заданием по занятию Vagrant

Для скачивания и запуска стенда:

```
git clone лабораторный стенд с выполненным домашним заданием
cd vagrant-provisioning-net-disks
vagrant up
```

Для создания этого репозитория были использованы команды:

```
[admin_insta11@mv334 vagrant-provisioning-net-disks]$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: will change to "main" in Git 3.0. To configure the initial branch name
hint: to use in all of your new repositories, which will suppress this warning,
hint: call:
hint:
hint: 	git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint: 	git branch -m <name>
hint:
hint: Disable this message with "git config set advice.defaultBranchName false"
Инициализирован пустой репозиторий Git в /home/admin_insta11/vagrant-provisioning-net-disks/.git/
[admin_insta11@mv334 vagrant-provisioning-net-disks]$ 
[admin_insta11@mv334 vagrant-provisioning-net-disks]$ git remote add origin https://github.com/kosogoroff/vagrant-provisioning-net-disks.git
[admin_insta11@mv334 vagrant-provisioning-net-disks]$ 
[admin_insta11@mv334 vagrant-provisioning-net-disks]$ git add .
[admin_insta11@mv334 vagrant-provisioning-net-disks]$ 
[admin_insta11@mv334 vagrant-provisioning-net-disks]$ git status
Текущая ветка: master

Еще нет коммитов

Изменения, которые будут включены в коммит:
  (используйте «git rm --cached <файл>...», чтобы убрать из индекса)
	новый файл:    Vagrantfile
	новый файл:    index.html

[admin_insta11@mv334 vagrant-provisioning-net-disks]$
[admin_insta11@mv334 vagrant-provisioning-net-disks]$ git commit -m "Занятие Vagrant - стенд с выполненным ДЗ"
[master (корневой коммит) 68ad0b8] Занятие Vagrant - стенд с выполненным ДЗ
 2 files changed, 209 insertions(+)
 create mode 100644 Vagrantfile
 create mode 100644 index.html
[admin_insta11@mv334 vagrant-provisioning-net-disks]$ git branch -M main
[admin_insta11@mv334 vagrant-provisioning-net-disks]$ 
admin_insta11@mv334 vagrant-provisioning-net-disks]$ git push -u origin main
Перечисление объектов: 4, готово.
Подсчет объектов: 100% (4/4), готово.
При сжатии изменений используется до 4 потоков
Сжатие объектов: 100% (4/4), готово.
Запись объектов: 100% (4/4), 3.37 KiB | 3.37 MiB/s, готово.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/kosogoroff/vagrant-provisioning-net-disks.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
[admin_insta11@mv334 vagrant-provisioning-net-disks]$
```
