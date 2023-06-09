# 10.6 «Disaster recovery»
# Александр Широбоков
## Задание 1. В чём разница между DRaaS, BaaS, Active-Active, Active-Passive?
DRaaS (Disaster Recovery as a Service) и BaaS (Backup as a Service) являются двумя различными подходами к обеспечению безопасности данных и их восстановлению в случае катастрофической потери.

 - DRaaS является формой облачного сервиса, который позволяет организациям восстанавливать данные и приложения после серьезных сбоев или катастроф. Это может включать восстановление серверов, баз данных и других важных компонентов информационной инфраструктуры. DRaaS предоставляет компаниям возможность быстро восстановить свою деятельность после непредвиденных сбоев и гарантировать бизнес-непрерывность.

 - BaaS, в свою очередь, ориентирован на резервное копирование данных и предоставление доступа к ним в случае необходимости. BaaS помогает организациям защитить свои данные от потери в результате атак хакеров, ошибок пользователей и технических сбоев. BaaS может включать резервное копирование файлов, баз данных и приложений, а также их восстановление в случае потери.

 - Active-Active и Active-Passive — это два разных подхода к обеспечению доступности системы. Active-Active представляет собой метод, при котором две или более копии приложений работают одновременно и обслуживают пользователей, что обеспечивает повышенную доступность и снижает риски сбоев. Active-Passive предполагает наличие главного и резервного серверов, где основной сервер обрабатывает запросы пользователей, а резервный сервер готов к работе, если основной сервер выйдет из строя. Когда основной сервер восстановится, резервный сервер перестает быть активным.

В целом, различия между DRaaS, BaaS, Active-Active и Active-Passive связаны с тем, какие задачи они выполняют и какие преимущества они предоставляют организациям в области безопасности и доступности данных и приложений.

## Задание 2. Компании нужно составить план восстановления в случае Disaster recovery.
Для решения этой задачи предлагаю использовать облачную инфраструктуру с услугой восстановления данных (DRaaS).

 - Шаг 1: Выбор провайдера облачных услуг и услуги DRaaS.

Выбрать провайдера облачных услуг с высоким уровнем надежности, который предоставляет услугу DRaaS для восстановления данных и приложений в случае катастрофы.

 - Шаг 2: Резервное копирование данных.

Создать резервные копии системного диска (C:) и диска с данными (D:), используя инструменты, предоставляемые провайдером облачных услуг. Резервные копии должны создаваться регулярно и автоматически.

 - Шаг 3: Синхронизация данных.

Синхронизировать данные на системном диске (C:) и диске с данными (D:) с помощью инструментов, предоставляемых провайдером облачных услуг. Синхронизация должна происходить каждый раз при создании резервных копий.

 - Шаг 4: Восстановление данных.

В случае катастрофы или потери данных, использовать услугу DRaaS для восстановления системного диска (C:) и диска с данными (D:). Услуга DRaaS обеспечивает быстрое и надежное восстановление данных и приложений в облаке. Восстановление должно быть произведено в течение 24 часов после аварии.

 - Шаг 5: Планирование потоков данных.

Организовать планирование потоков данных, чтобы снизить нагрузку на сеть в рабочее время с 9:00 до 18:00 в понедельник-пятницу. Для этого можно использовать инструменты, предоставляемые провайдером облачных услуг, для настройки расписания копирования и синхронизации данных.

 - Шаг 6: Оптимизация использования ресурсов.

Оптимизировать использование ресурсов, включая место на дисках и пропускную способность сети, чтобы гарантировать надежность и скорость восстановления данных и приложений в случае катастрофы. Обеспечить, чтобы компания имела запас в 10 терабайт места как на серверах, так и в облаке.

### Топология решения:

 - В данном случае, топология решения будет состоять из локального сервера с системным диском и диском с данными, который будет использоваться для создания резервных копий и синхронизации данных с облачным хранилищем, предоставляемым провайдером облачных услуг. В случае катастрофы или потери данных, восстановление будет производиться с помощью услуги DRaaS, предоставляемой провайдером облачных услуг. При этом, восстановленный сервер будет содержать системный диск и диск с данными, которые будут автоматически синхронизироваться с облачным хранилищем.

В результате, компания получит надежную и гибкую систему восстановления данных и приложений, которая будет обеспечивать быстрое и надежное восстановление данных в случае катастрофы. Кроме того, использование облачной инфраструктуры позволит оптимизировать использование ресурсов, включая место на дисках и пропускную способность сети, что позволит сократить расходы компании на восстановление данных.

## Задание 3. Используя программу R-sync, составьте конфигурацию для выполнения прошлой задачи.
### В данном случае использую Rsync в качестве клиента, файл конфигурации будет иметь вид:
``` 
# Конфигурация для R-sync
# Копирование системного диска на сервере
rsync -avz --delete /dev/sda1 <адрес облачного хранилища>:/backup/system/

# Копирование диска с данными на сервере
rsync -avz --delete /dev/sda4 <адрес облачного хранилища>:/backup/data/
```
