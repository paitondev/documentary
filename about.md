# 1. Настройка:

1. Библиотека Playwright может использоваться как универсальный инструмент автоматизации браузера, предоставляя мощный набор API для автоматизации веб-приложений как для синхронного, так и для асинхронного Python.

2. Установка Playwright pytest:

   UV:
   ```
   uv init
   uv add pytest-playwright
   playwright install
   ```

   PIP:
   ```
   pip install pytest-playwright
   playwright install
   ```

3. Обновление библиотеки:

   UV:
   ```
   uv add --upgrade pytest-playwright playwright
   ```

   PIP:
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
   
