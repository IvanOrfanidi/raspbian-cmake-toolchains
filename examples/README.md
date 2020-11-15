### Быстрый старт

#### CMakeLists.txt пример головного проекта.

#### vscode настройки VS Code при интеграция сборки с отладчиком.
##### Для поддержки отладки необходимо поставить плагин `Native Debug`
* https://marketplace.visualstudio.com/items?itemName=webfreak.debug.

##### cmake-kits.json
```javascript
[
    {
        "name": "GCC RASPBIAN",
        "toolchainFile": "raspbian-cmake-toolchains/raspbian-toolchain.cmake"
    }
]
```

##### launch.json
```javascript
{
    "configurations": [
        {
            "type": "gdb",
            "request": "attach", // Вид запуска
            "name": "Attach to gdbserver",
            // Путиь к gdb отладчику из пакета нативного компилятору GCC
            "gdbpath": "/home/orfanidi/raspi/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin/arm-linux-gnueabihf-gdb",
            "executable": "./build/main", // Путь к исполняемому файлу
            "target": "192.168.109.5:4444", // IP адрес и порт удаленного устройства
            "remote": true,
            "cwd": "${workspaceRoot}",
            "valuesFormatting": "parseText"
        }
    ]
}
```
