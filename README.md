# pgb
Резервное копирование баз данных PostgreSQL

Команда:  
`pgb [options] <backupdir>`  

Параметры запуска:  
`-C` Сжимать данные при передаче на удаленный хост  
     Актуально для несжатых данных и низкоскоростных каналов передачи  
`-F` Выгрузить в специальном архивном формате. Вывод сжимается gzip  
     Восстанавливается с помощью pg_restore  
`-L` Отключить логирование  
`-d` Включить в выходной файл команды удаления (DROP) объектов базы данных  
     перед командами создания (CREATE) этих объектов (--if-exists)  
     Не применяется для специального архивного формата  
`-Z <compress level>` Сжимать резервную копию. Указывается степень сжатия от 0 до 9  
`-i "<db1> [<db2>...[<dbN>]]"` Только базы данных по списку  
`-e "<db1> [<db2>...[<dbN>]]"` Исключить базы данных по списку  
`-c <countcopies>` Количество хранимых копий (по умолчанию 21)  
`-r <remotehost>` Резервное копирование на удаленный хост по ssh  
`-h <identifyfile>` Файл, из которого считывается ssh индентификатор (закрытый ключ) для проверки подлинности  

Примеры:  
`pgb /mnt/backup`  
Резервное копирование всех баз данных PostgreSQL в папку /mnt/backup  
  
`pgb -Z 6 /mnt/backup -i db.*`  
Резервное копирование баз данных PostgreSQL с названиями, начинающимися с db в папку /mnt/backup с сжатием 6 уровня  

`pgb -Z 6 /mnt/backup -e db.*`  
Резервное копирование баз данных PostgreSQL кроме с названиями, начинающимися с db в папку /mnt/backup с сжатием 6 уровня  

`pgb /mnt/backup -i "DB1 DB2"`  
Резервное копирование баз данных PostgreSQL DB1 и DB2 в папку /mnt/backup  
