# Гайд по **OhMyZsh**
[Ссылка на плагины](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins)  
[Ссылка на темы](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)

Для удаления **OhMyZsh** можно использовать команду:  
```
rm -rf ~/.oh-my-zsh
```

Команд для установки **.ohmyzsh** с методом curl:  
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

После выполнения комнанды файл кофигурации должен создатьс в домашней директории по такому пути /home/akim/.zshrc  
Для того, чтобы открыть проводник с текущим местоположением можно использовать команду:  
```
explorer.exe .
```

Для того, чтобы открыть файл конфигурации для редоктирования можно использовать следующую команду:  
```
nano ~/.zshrc
```

## Редактирование файла конфигурации и установка плагинов

### Первый плагин **zsh-autosuggestions**

Команда для установки плагина:  
```
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
``` 
Этот плагин будет установлен по данному пути: /home/akim/.oh-my-zsh/custom/plugins/zsh-autosuggestions  

Для подключения плагина сначала нужно открыть файл редактирования  
```
nano ~/.zshrc
plugins=(git zsh-autosuggestions) - найти строку с plugins и добавить туда сам плагин
source ~/.zshrc - применить изменения
``` 

### Второй плагин **zsh-syntax-highlighting**

Скачайте плагин в папку custom/plugins вашего Oh My Zsh:  
```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

И также в файле конфигурации к плагинам дописать:  
``` 
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```

### Третий плагин **Powerlevel10k**

[Ссылка на плагин](https://github.com/romkatv/powerlevel10k)
```
git clone https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k
```

Настройка темы:  
``` 
ZSH_THEME="powerlevel10k/powerlevel10k"
```
Репозиторий клонируется по данному пути /home/akim/.oh-my-zsh/custom/themes/powerlevel10k  
Если вы установили Powerlevel10k и хотите снова запустить мастер настройки (wizard), выполните следующую команду:
``` 
p10k configure
```

Для редактирования файла конфигурации **Powerlevel10k**
```
nano ~/.p10k.zsh
source ~/.zshrc - после нужно также сохранить файл и обновить настройки
```


