# 1. Установка
#### Через пакет uv:
```
uv self update
uv add playwright
playwright install
```
#### Через библиотеку pip:
```
pip install --upgrade pip
pip install playwright
playwright install
```
# 2. Использование.
#### После установки вы можете import запустить Playwright в виде скрипта на Python и использовать любой из 3 браузеров (chromium, firefox и webkit).
```
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch()
    page = browser.new_page()
    page.goto("https://playwright.dev")
    print(page.title())
    browser.close()
```
#### Playwright поддерживает два варианта API: синхронный и асинхронный. Если ваш современный проект использует asyncio , вам следует использовать асинхронный API:
```
import asyncio
from playwright.async_api import async_playwright

async def main():
    async with async_playwright() as p:
        browser = await p.chromium.launch()
        page = await browser.new_page()
        await page.goto("https://playwright.dev")
        print(await page.title())
        await browser.close()

asyncio.run(main())
```
# Первый сценарий.
#### В первом скрипте мы перейдем по ссылке playwright.dev/ и сделаем снимок экрана в WebKit.
```
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.webkit.launch()
    page = browser.new_page()
    page.goto("https://playwright.dev/")
    page.screenshot(path="example.png")
    browser.close()
```
#### По умолчанию Playwright запускает браузеры в хедлесс режиме. Чтобы увидеть пользовательский интерфейс браузера, установите параметр headless, False в значение.
```
firefox.launch(headless=False, slow_mo=50)
```

