# gulp-builder

## :zap: Установка
* установите [NodeJS](https://nodejs.org/en/) ***lts*** (на момент создания сборщика v16.13.2)
* скачайте сборку в консоли с помощью [Git](https://git-scm.com/downloads): ```git clone git@github.com:Garapov/frontend-builder.git #имя_проекта```
* перейдите в скачанную папку со сборкой: ```cd #имя_проекта```
* скачайте необходимые зависимости: ```npm install```
* чтобы начать работу, введите команду: ```npm run dev``` (режим разработки)
* чтобы собрать проект, введите команду ```npm run build``` (режим сборки)

Если вы всё сделали правильно, у вас должен открыться браузер с локальным сервером.

## :zap: Загрузка в новый репозиторий
* Создайте пустой репозиторий
* перейдите в скачанную папку со сборкой: ```cd #имя_проекта```
* запустите команду: ```git remote remove origin```
* далее следуйте интсрукции Github по загрузке существующей папки


## :open_file_folder: Файловая структура

```
gulp-html-starter
├── dist
├── src
│   ├── blocks
│   ├── files
│   ├── fonts
│   ├── img
│   ├── js
│   ├── scss
├── .env_example
├── package.json
├── gulpfile.js
└── .gitignore
```

* Корень папки:
    * ```.gitignore``` – запрет на отслеживание файлов Git'ом
    * ```.env_example``` – стартовый шаблон для переменных среды
    * ```gulpfile.js``` — настройки Gulp
    * ```package.json``` — список зависимостей
* Папка ```src``` - используется во время разработки:
    * БЭМ-блоки и компоненты: ```src/blocks```
    * Остальные файлы: ```src/files```
    * шрифты: ```src/fonts```
    * изображения: ```src/img```
    * JS-файлы: ```src/js```
    * SCSS-файлы: ```src/scss```
    * SVG иконки для генерации спрайта: ```src/svgicons```
* Папка ```dist``` - папка, из которой запускается локальный сервер для разработки (при запуске ```npm run dev```)
* Папка ```gulp``` - папка с Gulp-тасками и настройками

## :keyboard: Команды
* ```npm run dev``` - запуск сервера для разработки проекта
* ```npm run build``` - собрать проект с оптимизацией без запуска сервера

## :green_book: Переменные среды
* В корне папки с проектом есть файл ```.env.example```, для использования переменных среды нужно переименовать его в ```.env```.
    * ```PORT``` - переменная для переопределения порта для запуска локального сервера. Пример использования: ```PORT=3000```.
    * ```NGROK_AUTHKEY``` - переменная для ключа доступа [NGROK](https://ngrok.com/)

## :bulb: Рекомендации по использованию
### Компонентный подход к разработке сайтов
* каждый БЭМ-блок имеет свою папку внутри ```src/blocks/modules```
* папка одного БЭМ-блока содержит в себе один html-файл, один SCSS-файл и один JS-файл (если у блока используется скрипт)
    * html-файл блока импортируется в файл ```src/views/index.html``` (или в необходимый файл страницы, откуда будет вызываться блок)
    * SCSS-файл блока импортируется в файл ```src/blocks/modules/_modules.scss```
    * JS-файл блока импортируется в ```src/js/import/modules.js```

Пример структуры папки с БЭМ-блоком:
```
blocks
├── modules
│   ├── header
│   │   ├── header.html
│   │   ├── header.js
│   │   ├── header.scss
```

### Компоненты
* компоненты (например, иконки, кнопки) оформляются в html с помощью примесей
* каждый компонент имеет свою папку внутри ```src/blocks/components```
* папка одного компонента содержит в себе один html-файл, один SCSS-файл и один JS-файл (если у компонента используется скрипт)
    * html-файл компонента импортируется в файл главной страницы ```src/index.html``` (или в необходимый файл страницы, откуда будет вызываться компонент)
    * SCSS-файл компонента импортируется в файл ```src/blocks/components/_components.scss```
    * JS-файл компонента импортируется в файл ```src/js/import/components.js```

### Страницы проекта
* страницы проекта находятся в корне папки ```src/```
    * главная страница: ```src/views/index.html```

### Шрифты
* шрифты находятся в папке ```src/fonts```
    * шрифты автоматически подключаются в файл ```src/styles/base/_fonts.scss```
    * шрифты форматов ```{*.otf}``` автоматически конвертируются в формат ```{*.ttf}``` в папку с шрифтами ```src/fonts```
    * шрифты форматов ```{*.ttf}``` автоматически конвертируются в формат ```{*.woff, *.woff2}``` в папку с шрифтами в сборке ```dist/fonts```

### Изображения
* изображения находятся в папке ```src/img```
    * изображения автоматически конвертируются в формат ```.webp```.
    * изображения подключенные как ```<img src="@img/download.png" width="100" alt="">``` автоматически превращаются в ```<picture><source srcset="img/download.webp" type="image/webp"><img src="img/download.png" width="100" alt=""></picture>```.

### Сторонние библиотеки
* все сторонние библиотеки устанавливаются в папку ```node_modules```
* для их загрузки воспользуйтеcь командой ```npm install package_name```
* для подключения JS-файлов библиотек импортируйте их в самом начале JS-файла БЭМ-блока (то есть тот БЭМ-блок, который использует скрипт), например:
```javascript
import $ from "jquery";
```
* для подключения стилевых файлов библиотек импортируйте их в файл ```src/styles/vendor/_libs.scss```
* JS-файлы и стилевые файлы библиотек самостоятельно изменять нельзя


### Подсказки путей в VSCode
* Установить расширение ``` Path Autocomplete ``` 
* Нажать ``` ctrl+shift+p ``` и набрать:
* Анг: ``` Preferences: Open Settings (JSON) ``` Рус: ``` Параметры: Открыть параметры (JSON) ```
* Добавить к настройкам:
```
"path-autocomplete.pathMappings": {
    "@img": "${folder}/src/img",
    "@js": "${folder}/dist/js",
    "@scss": "${folder}/src/scss",
    "@css": "${folder}/dist/css",
}
```
* Должно быть что то вроде:
```
{
    // ВАШИ НАСТРОЙКИ,
    // ВАШИ НАСТРОЙКИ,
    // ВАШИ НАСТРОЙКИ,
    // ВАШИ НАСТРОЙКИ,
    // ВАШИ НАСТРОЙКИ,
    "path-autocomplete.pathMappings": {
        "@img": "${folder}/src/img",
        "@js": "${folder}/dist/js",
        "@scss": "${folder}/src/scss",
        "@css": "${folder}/dist/css",
    }
}
```


## :open_file_folder: Утилиты

### Всплывающие окна
* Чтобы сделать всплывающее окно нужно:
* Кнопке добавить ``` data-modal="КАКОЙ_ТО_ИДЕНТИФИКАТОР" ```
* К обертке всплывающего окна добавить ``` data-modal-id="КАКОЙ_ТО_ИДЕНТИФИКАТОР" ```
* При клике на кнопку будет добавляться класс ``` isOpened ``` к обертке всплывающего окна
* Изменить data атрибуты и класс можно в файле ``` src/js/app.js ```

```
modals: new Modals({
    modalsSelector: "data-modal", // data атрибут для кнопки
    modalsOpenerSelector: "data-modal-id", // data атрибут для всплывающего окна
    openedClass: "isOpened" // класс для добавления
})
```