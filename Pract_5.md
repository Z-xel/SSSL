# Практика №5
## Инфраструктура
Для выполнения работы были развернуты несколько виртуальных машин:
- ВМ с уязвимым приложением ![image](https://github.com/user-attachments/assets/3e910e98-299c-4fb8-8d0f-4087e67965f5)
- ВМ для проведения атак и сканирования

## Уязвимое приложение
Для проверки на уязвимости было поднято приложение OWASP Juice Shop, на котором можно удобно отработать все атаки
![image](https://github.com/user-attachments/assets/f7534673-32fb-4dc3-b2b9-e37e84e8d567)
Также на нем запущен Suricata с настроенными правилами на различные сетевые атаки
![image](https://github.com/user-attachments/assets/d15fe076-00e9-4d0e-b51b-b7a5726791e3)
## Вторая ВМ
Был развернут Wazuh
![image](https://github.com/user-attachments/assets/5dc8ded0-80c2-4288-a485-f71c4461ef71)
![image](https://github.com/user-attachments/assets/ee1a1c73-9c00-49cb-acd0-7be5b64d79bd)

Запущен скан через Yara с помощью набора правил для поиска web угроз:
![image](https://github.com/user-attachments/assets/df564251-025d-4944-ae6e-b475d7973778)
В выборку Suricata попалась атака SQL Injection:
![image](https://github.com/user-attachments/assets/e7b46028-a962-44c9-a5cb-039ac239ba7a)
Для предотвращения атаки необходимо как минимум настроить экранирование специальных символов и проверить бизнес логику приложения.
