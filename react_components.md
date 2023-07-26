#### Мои компоненты React.js

Кнопки:
```
# Отправка формы
ButtonSubmit 
    props.id
    props.caption
    props.color

# Простая кнопка принимает функцию onClick
ButtonSimple
    props.id
    props.caption
    props.color
    props.onClick

# Кнопка-ссылка
ButtonLink
    props.caption
    props.color
    props.href

# Кнопка отправляет специальный JSON запрос
ButtonCurl
    props.caption
    props.color
    props.Id
    props.IP
    props.Cmd
    Click()

# Кнопка отправляет специальный JSON запрос и специальный запрос на обновление в базе
ButtonCurlBase
    props.caption
    props.color
    props.Id
    props.IP
    props.Cmd
    Click()

# Кнопка открывает модальное окно (id окна передается в target, окно в children)
ButtonModal
    props.id
    props.caption
    props.color
    props.target
    props.children

# Кнопка открывает toggle окно (id окна передается в target, окно в children)
ButtonToggle
    props.id
    props.caption
    props.color
    props.target
    props.children

# Кнопка открывает toggle окно Debug (id окна передается в target, окно в children)
# Кнопка отправляет специальный JSON запрос
ButtonToggleDebug
    props.id
    props.caption
    props.color
    props.Id
    props.IP
    props.target
    props.children
    Click()
```
Строки состояния:
```
# Строка состояния получает сообщение из JSON запроса
MsgLine
    state.message
```
Контейнеры:
```
# Контейнер простой
ContainerSimple
    props.id
    props.children

# Контейнер toggle
ContainerToggle
    props.id
    props.caption
    props.children

# Контейнер modal
ContainerModal
    props.id
    props.caption
    props.children
```
Окна:
```
PanelDebug
TableDevice
Terminal

ModalAuth
ModalUpdateDevice
ModalDelDevice
ModalAddDevice
```


Панели навигации:
```
NavBar
Pagination
```
