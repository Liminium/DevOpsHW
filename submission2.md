1. Вот консольные команды и ответы на них:

C:\Users\Umion\Desktop\devopshw>git cat-file -p HEAD
tree e7207f28b699ba8692587090a6f7efa77ccde434
parent 7db866f495c5a40935350f7116ed058c85891b48
author Umion <geometrydashofzheka@gmail.com> 1770891055 +0300
committer Umion <geometrydashofzheka@gmail.com> 1770891055 +0300
gpgsig -----BEGIN SSH SIGNATURE-----
 U1NIU0lHAAAAAQAAADMAAAALc3NoLWVkMjU1MTkAAAAgbxGtpLfbU2kcIQ5RCjSciPGvep
 JKyjR+LD7275Z0vOMAAAADZ2l0AAAAAAAAAAZzaGE1MTIAAABTAAAAC3NzaC1lZDI1NTE5
 AAAAQAQ2oYZFpp83yNs+QbXz2tb5283dpkjTNqUAPkJjSx4mbDWYWXk5dLCkHngq4vYmJm
 VSraIkP7JeV5NwH5ZHIgI=
 -----END SSH SIGNATURE-----

Add test file

C:\Users\Umion\Desktop\devopshw>git cat-file -p e7207f28b699ba8692587090a6f7efa77ccde434
040000 tree 54071349dfafff914c8757496a29844fdb72ce1e    .github
100644 blob a4210048363c68b1a9fca2aaec800056ff96018e    test.txt
100644 blob 431e4252da3f523bcb023a001b05ff91be8c29c8    text.txt

C:\Users\Umion\Desktop\devopshw>git cat-file -p 431e4252da3f523bcb023a001b05ff91be8c29c8
"text"

C:\Users\Umion\Desktop\devopshw>git cat-file -p a4210048363c68b1a9fca2aaec800056ff96018e
"Test content"

C:\Users\Umion\Desktop\devopshw>git cat-file -p 54071349dfafff914c8757496a29844fdb72ce1e
100644 blob a450cd1a37f8c2ba34aa6f5ced291dbed2d78063    pull_request_template.md

C:\Users\Umion\Desktop\devopshw>git cat-file -p a450cd1a37f8c2ba34aa6f5ced291dbed2d78063
## Context
Here is some context

## Description
Here is some Description

## Changes in the codebase
Here is what changed

## Changes outside the codebase
The same

## Aditional information
Additional information

2. 

Когда мы исполняем git cat-file -p -1, мы получаем метаданные последнего коммита.
И он сохраняет и представляет собой состояние моей локальной директории и другой информации на момент этого коммита.
Сущность blob с уникальным id отождествляется с конкретным файлом, tree - с папкой, которая содержит и дргуие tree и блобы.

3. Наверное, в прошлом пункте я как раз и описал, как Git сохраняет информацию.

4. Примеры данных blob: 100644 a4210048363c68b1a9fca2aaec800056ff96018e    test.txt

10644 - права доступа файла
a4210048363c68b1a9fca2aaec800056ff96018e - хеш, по которому я могу получить данные самого файла test.txt на момент комита
test.txt - название файла

Пример данных tree:

040000 tree 54071349dfafff914c8757496a29844fdb72ce1e    .github
100644 blob a4210048363c68b1a9fca2aaec800056ff96018e    test.txt
100644 blob 431e4252da3f523bcb023a001b05ff91be8c29c8    text.txt

Собственно, просто рекурсивное отображение папки

Пример данных commit:

tree e7207f28b699ba8692587090a6f7efa77ccde434
parent 7db866f495c5a40935350f7116ed058c85891b48
author Umion <geometrydashofzheka@gmail.com> 1770891055 +0300
committer Umion <geometrydashofzheka@gmail.com> 1770891055 +0300
gpgsig -----BEGIN SSH SIGNATURE-----
 U1NIU0lHAAAAAQAAADMAAAALc3NoLWVkMjU1MTkAAAAgbxGtpLfbU2kcIQ5RCjSciPGvep
 JKyjR+LD7275Z0vOMAAAADZ2l0AAAAAAAAAAZzaGE1MTIAAABTAAAAC3NzaC1lZDI1NTE5
 AAAAQAQ2oYZFpp83yNs+QbXz2tb5283dpkjTNqUAPkJjSx4mbDWYWXk5dLCkHngq4vYmJm
 VSraIkP7JeV5NwH5ZHIgI=
 -----END SSH SIGNATURE-----

Add test file

tree - это та корневая папка
parent - предыдущий комит и его хэш
Потом подпись и сообщение комита

2.

Вот порядок команд, которые я выполнял, и пояснения к ним:

git reset -soft HEAD~1 - так указано в задании (дерево не изменилось, просто HEAD подвинул)
git reset -hard HEAD~1 - так указано в задании (подвинулся HEAD и все, что было после удалилось)
git reflog - так указано в задании
git log -oneline -2 - посмотрел последние два оставшиеся комита, чтобы узнать их хэши
git show a950f20 - посмотрел полный хэш комита
git reset -hard <reflog_hash>, куда вставил в <> полный хэш, полученный с предыдущего запроса
Таким образом, я сначала просто удалил из истории один комит, потом вернулся к позапрошлому и удалил его из истории.
Затем посмотрел историю движения HEAD, последний комит и его хэш, а затем вернулся по хэшу к этому комиту.

Сниппет reflog'a:

git reflog
a950f20 (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
40df3f5 HEAD@{1}: reset: moving to 40df3f57cc9a474ccb995a14352c7153723d93f2
40df3f5 HEAD@{2}: reset: moving to HEAD~1
e913cef HEAD@{3}: reset: moving to HEAD~1
4eaaa14 HEAD@{4}: commit: First commit
e913cef HEAD@{5}: commit: Third commit
40df3f5 HEAD@{6}: commit: Second commit
a950f20 (HEAD -> git-reset-practice) HEAD@{7}: commit: First commit
5bf0b26 HEAD@{8}: reset: moving to HEAD~1
182dfa1 HEAD@{9}: commit: First commit
5bf0b26 HEAD@{10}: reset: moving to HEAD~2
21f3a47 HEAD@{11}: commit: First commit
6f224d9 HEAD@{12}: reset: moving to HEAD~1
1ebc9a3 HEAD@{13}: reset: moving to HEAD~1
40c9061 HEAD@{14}: commit: Third commit
1ebc9a3 HEAD@{15}: commit: Second commit
6f224d9 HEAD@{16}: commit: First commit
5bf0b26 HEAD@{17}: commit: Third commit
dc4158b HEAD@{18}: commit: Third commit
5e3ef7c HEAD@{19}: commit: Second commit
d141ba7 HEAD@{20}: reset: moving to HEAD~1
80447d0 HEAD@{21}: reset: moving to HEAD~1
65f582b HEAD@{22}: commit: Third commit
80447d0 HEAD@{23}: commit: Second commit
d141ba7 HEAD@{24}: checkout: moving from main to git-reset-practice
0fa52a3 (main) HEAD@{25}: checkout: moving from git-reset-practice to main
d141ba7 HEAD@{26}: commit: First commit
0fa52a3 (main) HEAD@{27}: checkout: moving from main to git-reset-practice
0fa52a3 (main) HEAD@{28}: checkout: moving from labs to main

Snippet git log'a:

commit a950f20bf14adb7422255878db692f0d9d3416ad (HEAD -> git-reset-practice)
Author: Umion <geometrydashofzheka@gmail.com>
Date:   Thu Feb 12 14:09:40 2026 +0300

    First commit

commit 5bf0b26663b5fd5650d5c95ea9ec1254ecde0dee
Author: Umion <geometrydashofzheka@gmail.com>
Date:   Thu Feb 12 14:02:33 2026 +0300

    Third commit

commit dc4158b4faa8d5892421bee039b12fbc51489aba
Author: Umion <geometrydashofzheka@gmail.com>
Date:   Thu Feb 12 14:02:01 2026 +0300

    Third commit

commit 5e3ef7ca60ac6745974656e4561b94ff76b6a489
Author: Umion <geometrydashofzheka@gmail.com>
Date:   Thu Feb 12 14:01:55 2026 +0300

    Second commit

commit d141ba766ccc914829daf0af66a022f7be0f271d
Author: Umion <geometrydashofzheka@gmail.com>
Date:   Thu Feb 12 13:54:59 2026 +0300

    First commit
.






