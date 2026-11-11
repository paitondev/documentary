# 1. Настройка:
1. Библиотека Playwright может использоваться как универсальный инструмент автоматизации браузера, предоставляя мощный набор API для автоматизации веб-приложений как для синхронного, так и для асинхронного Python.

2. Установка Playwright pytest:

   ```
   uv init
   uv add pytest-playwright
   playwright install
   ```

   ```
   pip install pytest-playwright
   playwright install
   ```

3. Обновление библиотеки:

   ```
   uv add --upgrade pytest-playwright playwright
   ```

   ```
   pip install pytest-playwright playwright -U
   ```

4. Системные требования:

   - Python 3.8 или выше.
   - Windows 11+, Windows Server 2019+ или подсистема Windows для Linux (WSL).
   - macOS 14 (Sonoma) или более поздняя версия.
   - Debian 12 / 13, Ubuntu 22.04 / 24.04 / 26.04 (x86-64 или arm64).
     
5. Для запуска тестов используется:
   ```
   pytest
   ```

# 2. Написание тестов:
1. Начальные действия

   1. Большинство тестов начинаются с перехода на страницу по указанному URL. После этого тест сможет взаимодействовать с элементами страницы.

      ```
      page.goto("https://playwright.dev/")
      ```

      Playwright будет ждать, пока страница не достигнет состояния загрузки, прежде чем переходить к следующему шагу.

   2. Выполнение действий начинается с определения местоположения элементов. Для этого Playwright использует API локаторов. Локаторы представляют собой способ поиска элемента(ов) на странице в любой момент времени.

      Создаем локатор:
      ```
      get_started = page.get_by_role("link", name="Get started")
      ```

      Нажимаем на него (запускаем):
      ```
      get_started.click()
      ```

      Либо, в одну строку:
      ```
      page.get_by_role("link", name="Get started").click()
      ```
    3. В Playwright используются утверждения , которые будут ждать выполнения ожидаемого условия. Использование этих утверждений позволяет сделать тесты нестабильными и устойчивыми.
2. Основные действия:
    ```
    locator.check()               Установите флажок ввода.
    locator.click()               Нажмите на элемент.
    locator.uncheck()             Снимите флажок с поля ввода.
    locator.hover()               Наведите курсор мыши на элемент.
    locator.fill()                Заполните поле формы, введите текст.
    locator.focus()               Сфокусируйте элемент.
    locator.press()               Нажмите одну клавишу.
    locator.set_input_files()     Выберите файлы для загрузки.
    locator.select_option()       Выберите вариант в выпадающем списке.
    ```
3. Утверждения:
   ```
   expect(locator).to_be_checked()            Флажок установлен.
   expect(locator).to_be_enabled()            Управление включено.
   expect(locator).to_be_visible()            Элемент виден.
   expect(locator).to_contain_text()          Элемент содержит текст.
   expect(locator).to_have_attribute()        Элемент имеет атрибут.
   expect(locator).to_have_count()            Список элементов имеет заданную длину.
   expect(locator).to_have_text()             Элемент соответствует тексту.
   expect(locator).to_have_value()            Входной элемент имеет значение.
   expect(page).to_have_title()               Страница имеет заголовок.
   expect(page).to_have_url()                 Страница имеет URL.
   ```
# 3. Codegen, и его возможности. (Генерация текстов.)
Playwright может автоматически генерировать тесты, предоставляя быстрый способ начать тестирование. Codegen открывает окно браузера для взаимодействия и Playwright Inspector для записи, копирования и управления сгенерированными тестами.
   ```
   playwright codegen demo.playwright.dev/todomvc
   ```
   1. Запись теста.
   2. Генерация локаторов.
   3. Эмуляция.
# 4. Запуск и отладка тестов.
Запуск в браузере из playwright.config.
```
pytest
```
Запуск параллельно.
```
pytest --numprocesses 2
```
Запуск в моде HEADED.
```
pytest --headed
```
Запуск в разных браузерах.
```
pytest --browser webkit
```
Запуск отдельных тестов.
```
pytest test_login.py
```
Запуск файлов из разных дирректорий.
```
pytest tests/test_todo_page.py tests/test_landing_page.py
```
Запуск файлов с определенным словом, например (landing, login).
```
pytest -k test_add_a_todo_item
```
# 5. Трассировка
Playwright Trace Viewer — это графический инструмент, позволяющий просматривать записанные трассировки тестов Playwright, то есть вы можете перемещаться вперед и назад по каждому действию теста и визуально видеть, что происходило во время каждого действия.

Запись трассировки.
```
pytest --tracing on/off/retain-on-failure
```
Вы можете открыть сохраненный трассировочный файл с помощью Playwright CLI или в браузере trace.playwright.dev.
```
playwright show-trace trace.zip
```
# 6. Настройка CI.
В этом разделе мы рассмотрим запуск тестов на GitHub с помощью GitHub Actions.

Первым делом создаем папку .github/workflows, затем создаем файл playwright.yml.
Пример кода, приведённый ниже, чтобы ваши тесты запускались при каждом push/pull-запросе для основной/ветки master.
```
name: Playwright Tests
on:
  push:
    branches: [ main, master ]
  pull_request:
    branches: [ main, master ]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v6
    - name: Set up Python
      uses: actions/setup-python@v6
      with:
        python-version: '3.13'
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    - name: Ensure browsers are installed
      run: python -m playwright install --with-deps
    - name: Run your tests
      run: pytest --tracing=retain-on-failure
    - uses: actions/upload-artifact@v5
      if: ${{ !cancelled() }}
      with:
        name: playwright-traces
        path: test-results/
```
# 7. Справочник по плагину Pytest.
Playwright предоставляет плагин Pytest для написания сквозных тестов.

Для запуска тестов используйте Pytest CLI.
```
pytest --browser webkit --headed
```
Если вы хотите автоматически добавлять аргументы командной строки без их указания, вы можете использовать файл pytest.ini.
```
# content of pytest.ini
[pytest]
# Run firefox with UI
addopts = --headed --browser firefox
```
