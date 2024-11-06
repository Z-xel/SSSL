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











