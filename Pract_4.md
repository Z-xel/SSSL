# Практическая работа №4. Network Threat Hunting
Выполнил студент группы ББМО-01-23 Курдюков А.А.

## Часть 1.
![image](https://github.com/user-attachments/assets/f25f14b1-dc78-403c-b811-12637bd06143)

![image](https://github.com/user-attachments/assets/766d68e2-495e-4953-bbab-9ce899443dfb)

![image](https://github.com/user-attachments/assets/dd161135-279e-4357-8cd3-ac4174682de0)

![image](https://github.com/user-attachments/assets/f76b8965-8bc7-41c9-9a07-5cdd9d05bbe7)

Первая запись:
![image](https://github.com/user-attachments/assets/0fe1f689-a934-4b2e-beff-5054b82ea933)

Опишем первую запись:
- Очень высокий beacon score
- Множество подключений за 24 часа (3 011)
- Гистограмма довольно ровная
- Пользовательский агент идентифицируется как Windows 7
    Может быть легитимным, но явяляется устаревшим
- Нет строки хостинга
    Должно быть указано полное доменное имя веб - сервера

Вторая запись:
  ![image](https://github.com/user-attachments/assets/7c424db1-dcf6-452a-87af-681c65bc2b98)

Опишем вторую запись:
- Узел оптимизации доставки MS
- Используется в Windows для установки исправлений
- Цифровой сертификат вполне легитимный
- Можно внести в safelist

Третья запись:
![image](https://github.com/user-attachments/assets/81d14865-82cd-446d-9867-17a2b85a6f43)
Судя по всему это Windows tile services (Можно внести в safelist)

Четвертая запись:
![image](https://github.com/user-attachments/assets/e0ed5a42-7144-4697-98ab-5604b7b33965)

Windows patching - похожа на вторую запись, обе можно внести в safelist

Пятая:
![image](https://github.com/user-attachments/assets/53b7f101-3b11-476f-b5b4-6fbfe2ae7f91)

Аналогична предыдущей записи

Шестая:
![image](https://github.com/user-attachments/assets/a3bce323-c4bf-40d8-8d86-7985d756860f)

Аналогична предыдущей записи

Вывод: 
- Первая запись на общем фоне выглядит подозрительно
- Остальные выглядят легитимными:
    Windows patching
    Windows desktop tile services
- Внесем эти последние 5 записей в safelist

![image](https://github.com/user-attachments/assets/5b48ff87-fc98-49ed-a5a4-150b315b0407)

Итоговый safelist:
![image](https://github.com/user-attachments/assets/b504dd45-f617-44f0-8245-003199597901)

Далее рассмотрим длительные подключения:
![image](https://github.com/user-attachments/assets/e80bac84-9ca4-4a71-abe9-b88d3de75d17)

Здесь есть 2 записи, длительностью почти 24 часа.
Просмотрим первую через virustotal
![image](https://github.com/user-attachments/assets/71ef2ec1-b259-49b5-9600-a14d7ba9ac71)
![image](https://github.com/user-attachments/assets/87460a9d-d0a0-4718-bdfb-205880b1a59b)

По данному адресу находится знакомая форма
![image](https://github.com/user-attachments/assets/476dca4a-e6fa-468a-8322-b98f949da9f7)

Просмотрим вторую через virustotal
![image](https://github.com/user-attachments/assets/0e17dc81-1642-4eda-82d5-cbbebef6203c)
Данная запись явно связана с microsoft

Вернемся к самой первой подозрительной записи 

![image](https://github.com/user-attachments/assets/ed3d4d35-9502-4efc-975b-9a0b1268c056)


Наименьший размер сеанса, но наибольшее количество подключений. Возможно, это C2 heartbeat
И подтверждено отсутствие FQDN запроса перед подключением:
![image](https://github.com/user-attachments/assets/10199270-10c9-40be-8e77-8c7744021d7f)

Посмотрим логи: 
![image](https://github.com/user-attachments/assets/2d4ad26d-6b81-4f33-8679-3474611d10d0)

![image](https://github.com/user-attachments/assets/e62a32c8-6e86-4ff1-9900-72161e050439)

![image](https://github.com/user-attachments/assets/f01c9207-ed58-4613-9153-707323f00d7b)

Вывод: Соединения с кодом 104.248.234.238 явно зловредное
- Нет FQDN запросов
- 3011 соединений с атрибутами beacon strong
- Изменена строка агента пользователя
- Нет поля "host" в HTTP-заголовке
- Длинная запутанная строка URI
- Поиск в Google "rmvk30g" возвращает "Fiesta EK"
- Все остальные записи могут быть занесены в safelist

## Часть 2.

![image](https://github.com/user-attachments/assets/7eee1c8d-8f93-4999-9dad-0695bede3f2f)

![image](https://github.com/user-attachments/assets/54a654a8-ff5d-4722-a937-45576eeb2e87)

![image](https://github.com/user-attachments/assets/29dd5e90-0a77-4c23-9bfa-f2a2be2679ce)

![image](https://github.com/user-attachments/assets/06de1b04-4256-445b-8370-103453321d44)

Что видим:
- В списке нет отдельных IP-адресов
- Проверка в левом верхнем углу экрана указывает на необходимость проверки модуля DNS
- Имя хоста состоит из шестнадцатеричных символов
- Потенциальный C2 через DNS

## Часть 3.

![image](https://github.com/user-attachments/assets/58dc89aa-87fa-49aa-938f-935d6dd65c91)

![image](https://github.com/user-attachments/assets/c14134b6-ea4b-4876-87ce-b0ea7892cfd1)

Это не совсем домен Skype
Пользовательский агент - это "Internet Explorer". Недопустимый пользовательский агент.

![image](https://github.com/user-attachments/assets/a61073c4-c915-4d58-bca7-93fe8bf52f9e)

![image](https://github.com/user-attachments/assets/ad074773-1de1-499e-9e63-5af609bbef37)

Время выдержки соединения колеблется, просмотрим эту запись через virustotal

![image](https://github.com/user-attachments/assets/b4ce7fee-6d30-4601-bd61-a16b7e4eca51)







