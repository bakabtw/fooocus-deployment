# Fooocus-API installation

## Добавляем репозитории Nvidia
```
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
  && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
```

# Обновляем пакеты
```
sudo apt update
```

# Обновляем систему
```
sudo apt upgrade
```

# Устанавливаем зависимости
```
sudo apt install nvidia-container-toolkit docker.io docker-compose
```

# Разрешаем пользователю `ubuntu` работать с Docker
```
sudo usermod -aG docker ubuntu
```

# Перезагружаем ОС после обновления ядра
```
sudo reboot
```

# Настраиваем NVIDIA Container Toolkit
```
sudo nvidia-ctk runtime configure --runtime=docker
sudo systemctl restart docker
```

# Клонируем репозиторий
```
git clone https://github.com/bakabtw/fooocus-deployment
```

# Редактируем `.env`
```
nano fooocus-deployment/.env
```

Пример файла `.env` приведен ниже:
```
BASE_URL=http://81.94.159.37:8888
SENTRY_DSN=https://eb6e0859babea108edd6bd36b143822a@o4506291540852736.ingest.sentry.io/4506291542818816
```

- `BASE_URL` - URL для доступа к Fooocus-API (без "`/`" в конце)
- `SENTRY_DSN` - URL для отчётов Sentry

# Запускаем сервисы
```
cd fooocus-deployment/
docker-compose up -d
```
