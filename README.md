# Rofi — Catppuccin Mocha · app grid 4×4

Лаунчер для **Super+D** в связке **bspwm + sxhkd**.
Тёмная тема в палитре **Catppuccin Mocha**, приложения выводятся сеткой **4×4** (иконка над названием).

## Установка

```sh
# 1. Положить тему
cp rofi/config.rasi ~/.config/rofi/config.rasi

# 2. Перезапустить launcher (быстрое изменение темы)
rofi -config ~/.config/rofi/config.rasi -show drun
```

## Файлы

| Файл            | Назначение                                   |
|-----------------|----------------------------------------------|
| `rofi/config.rasi` | Тема rofi (конфиг + стили в одном файле)     |

## Что внутри

- **Сетка 4×4**: `listview { columns: 4; lines: 4; flow: horizontal }`, иконка над текстом (`element { orientation: vertical }`).
- **Иконки**: Papirus/Papirus, показ включён (`show-icons`).
- **Цвета**: Catppuccin Mocha (base `#1e1e2e`, mauve `#cba6f7`, текст `#cdd6f4`).
- **Режимы**: `drun,run,window` — переключение вкладками внизу (`mode-switcher`).
- **Поиск**: `fuzzy` matching, история, сортировка.

## Запуск из sxhkd

В `~/.config/sxhkd/sxhkdrc` строка уже есть:

```sh
super + d
    rofi -show drun -show-icons
```

Просто подставь `-config ~/.config/rofi/config.rasi`, если хочешь явно указать тему.
