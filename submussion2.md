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



