## Тестирование
Файлы с тестами должны находится в корне проекта в папке **tests**.

### Jest
Jest — это фреймворк для тестирования JavaScript/TypeScript.

Документация на русском: [ссылка](https://jestjs.io/ru/docs/getting-started#%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-%D0%B1%D0%B0%D0%B7%D0%BE%D0%B2%D0%BE%D0%B3%D0%BE-%D1%84%D0%B0%D0%B9%D0%BB%D0%B0-%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D0%B8)

Установка:
`yarn add --dev jest`

#### Конфигурация
Файл конфигурации `jest.config.cjs` должен находиться в корне проекта.

Создание базового конфига для проектов на JavaScript: `yarn create jest@latest`

Конфиг для проектов на TypeScript:
```
/** @type {import('ts-jest').JestConfigWithTsJest} */
module.exports = {
    preset: "ts-jest",
    testEnvironment: "jsdom",
    transform: {
        "^.+\\.tsx?$": [
            "ts-jest",
            {
                diagnostics: {
                    ignoreCodes: [1343],
                },
                astTransformers: {
                    before: [
                        {
                            path: "./node_modules/ts-jest-mock-import-meta",
                            options: { metaObjectReplacement: { url: "https://www.url.com" } },
                        },
                    ],
                },
            },
        ],
    },
    transformIgnorePatterns: ["<rootDir>/node_modules/"],
};

```
