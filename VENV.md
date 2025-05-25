# Step 1: Installation Poetry on Linux (Ubuntu)
The Poetry website offers an official installation script that is used to set up Poetry.

Run this command to initiate the download of the installation script and Poetry installation.   
`curl -sSL https://install.python-poetry.org | python3 -`
- Once the installation is complete, modify your PATH environment variable so that you can use Poetry from the command line. For this, open the ~/.bashrc file using nano.   
`nano ~/.bashrc`
- At the end of the file, add the following path:    
`export PATH="/home/ubuntu/.local/bin:$PATH"` <!-- Instead of ubuntu use your username -->
- Incorporate and save the changes into your current session:   
`source ~/.bashrc`
- Print the current version of Poetry to verify if you can run its commands:   
`poetry --version`  


# Шаг 1: Установка Poetry на Linux (Ubuntu)
Сайт Poetry предлагает официальный установочный скрипт, который используется для настройки Poetry.

Выполните эту команду, чтобы начать загрузку установочного скрипта и установку Poetry.  
`curl -sSL https://install.python-poetry.org | python3 -`

- После завершения установки измените переменную окружения PATH, чтобы можно было использовать Poetry из командной строки.   
`echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc` 
- Включите и сохраните изменения в текущем сеансе:   
`source ~/.bashrc`
- Узнайте текущую версию Poetry, чтобы проверить, можете ли вы выполнить ее команды:   
`poetry --version`

# Шаг 2: Создание проекта и виртуального окружения
- Создаем папку проекта   
`mkdir my-project && cd my-project`
- Инициализируем Poetry   
`poetry init`
- Создаем виртуальное окружение   
`poetry install --no-root` # Пропускаем установку текущего проекта как пакета
- Добавляем pre-commit как dev-зависимость   
`poetry add pre-commit --group dev`
- Создаем конфиг pre-commit   
`touch .pre-commit-config.yaml`
- В конфиг файл добавляем:   
```
repos:
  # Общие проверки
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.5.0
    hooks:
      - id: check-yaml           # Валидация YAML
      - id: end-of-file-fixer     # Исправление конца файлов
      - id: trailing-whitespace   # Удаление пробелов в конце строк

  # Python
  - repo: https://github.com/psf/black
    rev: 23.12.1
    hooks:
      - id: black                # Форматирование кода

  - repo: https://github.com/pycqa/flake8
    rev: 6.1.0
    hooks:
      - id: flake8               # Линтинг кода

  # YAML
  - repo: https://github.com/adrienverge/yamllint.git
    rev: v1.33.0
    hooks:
      - id: yamllint             # Линтинг YAML
        args: [--strict]

  # Docker
  - repo: https://github.com/hadolint/hadolint
    rev: v2.12.0
    hooks:
      - id: hadolint             # Линтинг Dockerfile
```      
- Устанавливаем линтеры   
`poetry add black flake8 yamllint --group dev`
- Устанавливаем hadolint для Docker   
```
sudo curl -L https://github.com/hadolint/hadolint/releases/latest/download/hadolint-Linux-x86_64 -o /usr/local/bin/hadolint

sudo chmod +x /usr/local/bin/hadolint
```   
- Инициализируем pre-commit   
`poetry run pre-commit install`
- Запускаем проверки   
`poetry run pre-commit run --all-files`

# Шаг 3: Работа с проектом

Для активации виртуального окружения:   
`poetry shell`   
Для выхода из окружения:   
`exit`