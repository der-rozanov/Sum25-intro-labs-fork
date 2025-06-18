# Отчёт по лабораторной работе 3: CI/CD с GitHub Actions

## Задание 1: Создание базового CI-пайплайна

### Выполненные шаги:
1. Создал структуру файлов:

   ``` 
    mkdir -p .github/workflows
    New-item .github/workflows/github-actions-demo.yml 
   ```

2. Скопировал туда yaml код из примера

3. Запушил в ветку Lab3 

4. В actions наблюдаю вывод информации которая была получена. Файл приложен - 0_Explore-GitHub-Actions.txt

здесь все было просто и понятно

## Задание 2: Создание ручного триггера и получение информации о системе

### Выполненные шаги:

1. Изменил метод запуска с push на workflow_dispatch:

2. Добавил несколько команд на получение изформации о системе 

    ```
    - name: Gather system info
        run: |
          echo "=== 🖥️ System Information ==="
          echo "OS: $(lsb_release -d | cut -f2)"
          echo "Kernel: $(uname -a)"
          echo "CPU: $(nproc) cores, $(lscpu | grep 'Model name' | cut -d':' -f2 | xargs)"
          echo "RAM: $(free -h | grep Mem | awk '{print $2}')"
          echo "Disk: $(df -h | grep -vE 'tmpfs|udev' | awk '{print $1 " " $4}')"
          echo "Runner: ${{ runner.os }} (${{ runner.name }})"
          echo "============================"
    ```

3. Таким образом объединив две задачи по настройке ручного триггера и поиска информации о системе. 

4. В этом задании был нюанс, заключающися в том, что ручной триггер заработал только из maser ветки, поэтому его пришлось пушить оттуда. Тем не менее ручной триггер запустил action с выходом который представлен в файле get-info logs.txt


