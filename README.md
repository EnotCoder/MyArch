# Archcraft — конфиги

Конфиги для **Archcraft (bspwm + sxhkd)**.

---

## Rofi — Catppuccin Mocha · app grid 4×4

Лаунчер для **Super+D** в связке **bspwm + sxhkd**.
Тёмная тема в палитре **Catppuccin Mocha**, приложения выводятся сеткой **4×4** (иконка над названием).

### Установка

```sh
# 1. Положить тему
cp rofi/config.rasi ~/.config/rofi/config.rasi

# 2. Перезапустить launcher (быстрое изменение темы)
rofi -config ~/.config/rofi/config.rasi -show drun
```

### Что внутри

- **Сетка 4×4**: `listview { columns: 4; lines: 4; flow: horizontal }`, иконка над текстом (`element { orientation: vertical }`).
- **Иконки**: Papirus, показ включён (`show-icons`).
- **Фолбэк-иконка**: `application-fallback-icon: "application-x-executable"` — программам без иконки подставляется иконка «исполняемый файл».
- **Цвета**: Catppuccin Mocha (base `#1e1e2e`, mauve `#cba6f7`, текст `#cdd6f4`).
- **Режимы**: `drun,run,window` — переключение вкладками внизу (`mode-switcher`).
- **rofi 2.0**: режимы задаются через `modes:` (`modi:` оставлен для совместимости со старыми версиями). Комментарии только в формате `/* */` — строка с `#` ломает парсер rofi 2.0.
- **Поиск**: `fuzzy` matching, история, сортировка.

---

## Polybar — скруглённые углы

Бары **top** и **top_external** (2 монитора), палитра из `xrdb`.

Скругление реализует **picom** (`corner-radius = 10`), а не сам polybar:
из `rounded-corners-exclude` убран `window_type = 'dock'` — иначе панель
(окно типа `_NET_WM_WINDOW_TYPE_DOCK`) исключалась из скругления.

### Установка

```sh
cp polybar/config.ini polybar/colors.ini polybar/modules.ini polybar/launch.sh ~/.config/polybar/
cp bspwm/picom_configurations/1.conf ~/.config/bspwm/picom_configurations/1.conf
# перезапуск
killall polybar picom
~/.config/polybar/launch.sh &
picom --config ~/.config/bspwm/picom_configurations/1.conf &
```

### Что внутри

- Бары `top` / `top_external`: ширина 98%, `offset-x 1%`, `offset-y 0.5%`, высота 26 + бордюры 7.
- Фон `background = ${xrdb:background}`, шрифты JetBrainsMono Nerd Font + Material Design Icons.
- Палитра `colors.ini` привязана к `xrdb` (цвета терминала и панели совпадают).
- picom: `corner-radius = 10.0`, анимации (open/close/geometry), тени.

---

## Файлы

| Файл                                       | Назначение                                |
|--------------------------------------------|-------------------------------------------|
| `rofi/config.rasi`                         | Тема rofi (конфиг + стили в одном файле)  |
| `polybar/config.ini`                       | Конфиг баров (top / top_external)         |
| `polybar/colors.ini`                       | Палитра polybar (из xrdb)                 |
| `polybar/modules.ini`                      | Модули polybar                            |
| `polybar/launch.sh`                        | Запуск polybar под 1/2 монитора           |
| `bspwm/picom_configurations/1.conf`        | picom: скругление углов + анимации        |

## Запуск из sxhkd

Rofi — `super + d` → `rofi -show drun -show-icons` (тема из `~/.config/rofi/config.rasi`).
Polybar и picom стартуют из автозапуска Archcraft (`bspwmrc` / autostart).