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

# Создаем необходимые папки для кэша
```
mkdir ~/repositories
mkdir -p ~/.cache/pip
```

# Запускаем контейнер
```
docker run --gpus=all -e NVIDIA_DRIVER_CAPABILITIES=compute,utility -e NVIDIA_VISIBLE_DEVICES=all \
    -v ~/repositories:/app/repositories \
    -v ~/.cache/pip:/root/.cache/pip \
    -p 8888:8888 konieshadow/fooocus-api
```
