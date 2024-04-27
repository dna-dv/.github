## Инструменты

### Yarn

В качестве пакетного менеджера используется **yarn**.
Yarn устанавливается с помощью **npm**.

Установка: `npm install --global yarn`.

Пример установки пакетов:

`yarn add lodash` для установки в общие зависимости.

`yarn add lodash --dev` для установки в зависимости при разработке.
***

### JSDoc

Для документации кода используется пакет **JSDoc**.

**Основные теги JSDoc**:

    @param: Описывает параметры функции.
    @returns: Описывает возвращаемое значение функции.
    @type: Указывает тип данных.
    @description: Предоставляет дополнительное описание.
    @example: Предоставляет пример использования функции или метода.

**Пример документирования функции:**

```
/**
 * @function unixTimeToFormattedTime
 * @description Преобразует unixTimestamp в формат "чч:мм:сс".
 * @param {number} unixTimestamp - Временная метка Unix в миллисекундах.
 * @returns {string} Отформатированное время в формате "чч:мм:сс".
 */
export default function unixTimeToFormattedTime(unixTimestamp: number): string {
    const date = new Date(unixTimestamp * 1000);

    const hours = date.getHours().toString().padStart(2, '0');
    const minutes = date.getMinutes().toString().padStart(2, '0');
    const seconds = date.getSeconds().toString().padStart(2, '0');

    return `${hours}:${minutes}:${seconds}`;
}
```

Установка: `yarn add jsdoc --dev`

Для сборки документации проекта используется следующая команда `npx jsdoc -c [путь до файла конфигурации]` 

**Конфигурация JSDoc:**
```
{
  "source": {
    "includePattern": ".+\\.js(doc|x)?$",
    "include": ["."],
    "exclude": ["node_modules"]
  },
  "recurseDepth": 10,
  "opts": {
    "destination": "./docs/",
    "recurse": true
  }
}
```

### Vite

Для сборки проектов используется **Vite**.

Установка: `yarn add vite --dev`

**Основные команды:**

* `vite --open` - запуск проекта на локальном сервере
* `vite build --emptyOutDir` - сборка проекта с флагом очищения директории сборки

Конфигурационный файл `vite.config.js` должнен находиться в корне проекта.

**Стандартный конфигурационный файл:**
```
import { defineConfig } from 'vite';
import { minifyTemplateLiterals } from 'rollup-plugin-minify-template-literals';

export default defineConfig({
    clearScreen: false,
    server: {
        port: 5000,
        strictPort: true,
    },
    root: './resources',
    base: '',
    envPrefix: ['VITE_'],
    build: {
        outDir: '../build',
    },
    esbuild: {
        supported: {
            'top-level-await': true,
        },
    },
    plugins: [minifyTemplateLiterals()],
    define: {
        'process.env': {},
    },
});

```