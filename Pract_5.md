# Практика №5
## Инфраструктура
Для выполнения работы были развернуты несколько виртуальных машин:
- ВМ с уязвимым приложением ![изображение](https://github.com/user-attachments/assets/59867b3d-a4f0-4484-b2b6-5326058e1907)
- ВМ для проведения атак и сканирования

## Уязвимое приложение
Для проверки на уязвимости было поднято приложение OWASP Juice Shop, на котором можно удобно отработать все атаки
![изображение](https://github.com/user-attachments/assets/027b5123-3b95-4ad4-9463-33dbb11db783)
Также на нем запущен Suricata с настроенными правилами на различные сетевые атаки
![изображение](https://github.com/user-attachments/assets/64d4719c-ad82-44d8-b3a4-03c18236de92)
## Вторая ВМ
Был развернут Wazuh
![изображение](https://github.com/user-attachments/assets/8b9b3c21-63b2-424b-93f9-c36e0709462c)
![изображение](https://github.com/user-attachments/assets/bfd0f68b-4742-45f2-b274-f1c9fad4ea38)
Также установлен сканер уязвимостей Nessus, запущенная задача сканирования:
![изображение](https://github.com/user-attachments/assets/1baaa72a-9b8f-48d4-94bf-7de719d2ad26)
Запущен скан через Yara с помощью набора правил для поиска web угроз:
![изображение](https://github.com/user-attachments/assets/9893c3ba-bb54-4b13-8107-725246e82960)
В выборку Suricata попалась атака SQL Injection:
![изображение](https://github.com/user-attachments/assets/ccbca492-6039-4548-9855-9dca7a96fb45)
Для предотвращения атаки необходимо как минимум настроить экранирование специальных символов и проверить бизнес логику приложения.
