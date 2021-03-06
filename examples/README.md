### Быстрый старт

* `CMakeLists.txt` пример проекта.

* `.vscode` настройки VS Code при интеграция сборки с отладчиком.

Для поддержки отладки необходимо поставить плагин [Native Debug](https://marketplace.visualstudio.com/items?itemName=webfreak.debug).
При отладке методом `launch` необходимо регать ключ для синхронизации исполняемого файла на удаленном устройстве
`ssh-copy-id -i /home/pi/.ssh/id_rsa.pub orfanidi@192.168.109.30`.

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
        },
        {
            "type": "gdb",
            "request": "launch", // Вид запуска
            "name": "Launch to gdbserver",
            // Путь к gdb отладчику
            "gdbpath": "/usr/bin/gdb",
            "target": "./main",
            "cwd": "${workspaceRoot}",
            "valuesFormatting": "parseText",
            "ssh": {
                "forwardX11": true,
                "host": "192.168.109.5", // IP адрес удаленного устройства
                "cwd": "/home/pi/Raspi-CMake/build/", // Путь к исполняемому файлу
                "user": "pi",
                "password": "gecHoop3",
                "x11host": "localhost",
                "x11port": 4444,
                // Синхронизация исполняемого файла на удаленном устройстве(необходимо регать ключ)
                "bootstrap": "rsync -avz orfanidi@192.168.109.30:/home/orfanidi/Raspi-CMake/build/main /home/pi/Raspi-CMake/build"
            }
        }
    ]
}
```
