<div align="center">
    <img height="200px" src="https://upload.wikimedia.org/wikipedia/commons/8/85/Kharkiv_Polytechnic_Institute.jpg?20150321192409"/>
</div>


# Шаблон звітів в LaTeX для студентів ХПІ

Цей проєкт створений для студентів ХПІ, щоб швидко і зручно створювати звіти для різних завдань, таких як лабораторні роботи, контрольні та інші навчальні роботи. Він дозволяє автоматизувати процес створення звіту, підставляючи ваші персональні дані та іншу необхідну інформацію в готовий шаблон звіту.

## Вимоги

Для використання проєкту вам потрібно мати:

### Збірка в Docker (_Рекомендовано_)

- `GNU Make` (для автоматизації збірки проєкту)
- `Docker` (для збірки звітів в вже налаштованому середовищі)
- `Docker Compose` (для запуска Docker контейнера з потрібними параметрами)

### Локальна збірка

- `GNU Make` (для автоматизації збірки проєкту)
- `LaTeX` (з установленими базовими пакетами, наприклад, `texlive` або інші)


## Налаштування

Щоб налаштувати звіт під себе, відкрийте файл `settings.tex` і заповніть його своїми даними. Ось приклад вмісту `settings.tex`, який ви маєте змінити:

```latex
\newcommand{\fullName}{ПІБ}
\newcommand{\studyingGroup}{КН-777а}
\newcommand{\variant}{7}

\newcommand{\tacherPosition}{Посада викладача}
\newcommand{\tacherFullName}{ПІБ викладача}
\newcommand{\subject}{Назва предмету}
\newcommand{\department}{Назва катедри}

\newcommand{\taskName}{Назва звіту}
% шлях до вашого файлу зі звітом який ви можете розміщувати в теці reports
\newcommand{\reportMainFile}{templates/lab/main.tex}
```

## Збірка
Після того, як ви заповнили свої дані та налаштували проєкт під себе, ви можете зібрати звіт, виконавши команду:

### Збірка в Docker (_Рекомендовано_)
```bash
make
```

### Локальна збірка
```bash
make build_locale
```

Після збірки ви побачите теку **build** в корені проєкту та зможете забрати звідти як готовий PDF документ так і інші файли білда
