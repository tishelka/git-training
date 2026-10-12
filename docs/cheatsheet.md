# Шпаргалка: Git под рукой

Не нужно учить все команды наизусть. Гораздо полезнее понять, в какой ситуации какую использовать.

## Где я сейчас?

| Команда | Для чего |
| --- | --- |
| `git status` | Что изменилось и что готово к коммиту |
| `git branch --show-current` | В какой ветке я сейчас |
| `git log --oneline -5` | Последние пять коммитов |
| `git diff` | Что поменялось, но ещё не добавлено через `git add` |
| `git diff --cached` | Что попадёт в ближайший коммит |
| `git remote -v` | Куда настроена отправка кода |

## Скачать проект и обновиться

```bash
git clone https://github.com/tishelka/git-training.git
cd git-training
git switch master
git pull --ff-only origin master
```

`git clone` нужен обычно один раз. `git pull --ff-only` забирает свежую общую ветку без автоматического merge-коммита. Если Git не может сделать fast-forward, не паникуйте — смотрите [разбор ошибок](troubleshooting.md).

## Ветки

```bash
git branch
git switch -c practice/yourname-task
git switch master
```

`git switch -c` создаёт **новую** ветку и сразу переводит вас в неё. Без `-c` переключает на уже существующую.

## Зафиксировать работу

```bash
git status
git add students/yourname.md
git commit -m "Add profile"
git push -u origin practice/yourname-task
```

При следующих коммитах в уже опубликованную ветку обычно достаточно `git push`.

**Разница:** `add` — выбирает файлы, `commit` — сохраняет контрольную точку локально, `push` — отправляет коммиты на GitHub.

## Подтянуть изменения, не теряя ориентации

```bash
git fetch origin
git log --oneline --all -8
git merge origin/master
```

`fetch` только получает информацию и коммиты с сервера, не меняя ваши рабочие файлы. `merge` пытается объединить изменения с текущей веткой.

## Полезные безопасные действия

```bash
git restore --staged students/yourname.md
git diff --check
git status
```

`restore --staged` уберёт файл **из индекса**, но сохранит его содержимое на компьютере.

Осторожно с `git restore path` без `--staged`: эта команда может отбросить незакоммиченные изменения файла. Не запускайте её, если не уверены.

## Мини-словарик

- **Repository:** папка с проектом и историей Git.
- **Commit:** зафиксированное состояние изменений.
- **Branch:** отдельная линия работы.
- **origin:** обычно имя удалённого репозитория на GitHub.
- **Pull Request:** просьба рассмотреть изменения перед включением в общую ветку.
- **Merge:** объединение изменений двух веток.
- **Conflict:** ситуация, когда Git не может решить, какие правки оставить.

[README](../README.md) · [Ошибки и решения](troubleshooting.md)
