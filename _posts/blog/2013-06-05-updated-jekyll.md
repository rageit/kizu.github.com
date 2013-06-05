---

categories: blog

layout: post

published: true

invisible: true

---

# Обновлённый Jekyll

Недавно Jekyll стал совсем большим — [была выпущена](https://github.com/blog/1502-jekyll-turns-1-0) версия «1.0».

В [ченджлоге](https://github.com/mojombo/jekyll/blob/master/History.markdown#100—2013-05-06) довольно много изменений: есть как новые фичи, так и всяческие исправления. О том, что критично знать про это обновление, можно прочитать в [этой статье](http://jekyllrb.com/docs/upgrading/).

Я перевёл свой сайт на эту версию. Ну, как перевёл, — всё и так работало, но зато появилась возможность многое сделать оптимальнее. Напишу немного о том, что же лично для меня интересного появилось в Jekyll 1.0.

## `page.path`

Это одна из тех вещей, которых я ждал от новой версии Джекила, — я даже в своё время [попинал](https://github.com/mojombo/jekyll/issues/633#issuecomment-11678912) лишний раз разработчиков комментариями к соответствующему ишью.

У старой версии Джекила была одна проблема — в информации о постах и страницах отсутствовала переменная с путём к исходнику. Почему это важно: для блога или сайта, выложенного на Гитхаб, очень полезным может быть предоставление быстрой возможности что-то поправить (форкнуть). Для этого можно на странице разместить ссылку либо напрямую на Гитхаб, либо, например, на prose.io или другой подобный сервис. В этой ссылке прописывается путь к исходнику страницы, которую нужно отредактировать; раньше в отсутствие соответствующей переменной приходилось такими-то хаками этот урл собирать вручную.

Теперь же всё просто: в данных страниц и постов стала доступна переменная `path`, в которую кладётся относительный путь к исходнику. Ура :)

## Абсолютные пермалинки

Пермалинки, задаваемые постам в YAML-заголовках, раньше были относительными. При этом не было возможности указать пермалинк уровнем выше — нельзя было использовать `../` (ну, или я так и не смог найти способ, как это можно было сделать). В новой версии Джекила теперь можно использовать и абсолютные урлы. Точнее, в 1.0 абсолютные урлы надо специально включать в конфиге директивой `relative_permalinks: false`, а с 1.1 это будет работать по умолчанию. Это значит, что, если сейчас вы используете относительные урлы (и не собираетесь их переделывать на абсолютные), надо явно указать `relative_permalinks: true`, чтобы в 1.1 ничего не сломалось.

Абсолютные урлы позволили мне чуть упростить файловую структуру репозитория — вынести все индексные страницы в отдельную папку, например.

## Изменившийся синтаксис CLI

В новом Джекиле изменился и формат вызова из командной строки, в том числе появилась возможность использовать дополнительные конфиги.

Например, теперь, чтобы запустить сервер Джекила, используя и дефолтный конфиг `_config.yml`, и дополнительный, скажем, `_config-dev.yml`, нужно запускать его так:

    jekyll serve --config _config.yml,_config-dev.yml

Таким образом, можно довольно просто настроить разработческое окружение, в котором, например, менять абсолютные урлы на локальные, включать отображение черновиков и вообще изменять что угодно независимо от продакшн-версии.

Стоит заметить, что в Jekyll 1.0 был объявлен ещё один ключ запуска: `--baseurl`, с помощью которого можно было бы менять переменную `baseurl`, но, во-первых, у меня не получилось ей воспользоваться: Джекилл вообще отказывался что-либо генерить с этой изменённой переменной, во-вторых, всё то же самое можно сделать, используя дополнительный конфиг, так что я пока не вижу смысла в ключе `--baseurl`.

## Черновики

В новом Джекиле появилась возможность использовать черновики. Если создать папку `_drafts`, то по умолчанию её содержимое будет игнорироваться, но, если запустить Джекил с ключом `--drafts`, содержимое этой папки будет распознано почти аналогично содержимому `_posts`. Полезное исключение: в таких постах не нужно указывать дату, таким образом для публикации нужно будет всего лишь переместить и переименовать файл со статьёй.

Я сам пока _такие_ черновики не использую, но, возможно, начну.

## Остальное

В ченджлоге можно [прочитать](https://github.com/mojombo/jekyll/blob/master/History.markdown#minor-enhancements-3) обо всём, что ещё поменялось, там довольно много всего, но больше ничего особо критичного.

В общем, я перешёл на новый Джекил, всё работает, всем рекомендую.