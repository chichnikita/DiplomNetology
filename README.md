#  Дипломная работа по профессии «Системный администратор»

Техническое задание : [Диплом sys-22](https://github.com/chichnikita/DiplomNetology/blob/main/Read_tx.md)  
Данный по подключениям к серверам : [INFO](https://github.com/chichnikita/DiplomNetology/blob/main/info.md)

## Инфраструктура
Для развёртки инфраструктуры использую Terraform и Ansible.
 * Terraform - смотрите terraform/main.ft и все прилагающие к нему файлы
 * Описывать метод подключения terraform к yandex cloud не буду - все было в лекциях, вебинарах и домашних заданиях, там все очень грамматно и четко показывали и объясняли.


Использовал следующий принцип работы, создал два каталога, на одном стоит сервер terraform, на другом разваричиваются сервера из terraform.

   ![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/95ea0227-5d94-4ee8-8567-de544738de46)


## Разворачиваем инфраструктуру используя Terraform 
   ![alt text](https://github.com/chichnikita/DiplomNetology/blob/main/img/Terraform_Init_Validate_Fmt.png?raw=true)
   
   ![alt text](https://github.com/chichnikita/DiplomNetology/blob/main/img/Terraform_Apply.png?raw=true)
   
   ![alt text](https://github.com/chichnikita/DiplomNetology/blob/main/img/Terraform_Apply_End.png?raw=true)
   ![alt-text](https://github.com/chichnikita/DiplomNetology/blob/main/img/gif/Terraform_Apply.gif)
   
Использовал минимальные конфигурации ВМ:2 ядра 20% Intel ice lake, 2-4Гб памяти, 10hdd, прерываемая.
## Проверяем параметры созданых виртуальных машин
   ![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/283d0070-4b4c-4640-adba-82964b9b4271)

Отдельно я создал сервер bastion-host он ничем не отличается от bastion-host1. Это была временна необходимость, так как при использовании команды terraform destcroy - удалялся сервер с bastion-host1(где лежит весь ansible).
Для того, что каждый раз не перекидывать файлы и заново устаналивать ansible и я поступил таким образом.
## Сайт
### Проверяем созданую Target Group
![1-20](./img/tg.png)
### HTTP router
![1-21](./img/router.png)
### Backend Group
![1-22](./img/bg.png)
### Balancer
![1-22](./img/Balancer.png)
### Проверяем созданую группу безопасности
![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/b6e4b99b-3b69-4cdc-acae-3e0f73185ed9)
### С помощью Ansible проверяем доступность созданых виртуальных машин
![1-23](./img/Ansible_Ping_All_Host.png)  
### Для ansible inventory использовал fqdn имена виртуальных машин в зоне ".ru-central1.internal"  
 ![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/278bb7fc-3ca6-4a10-bcff-92ad8c1dffd4)  

### Устанавливаем Nginx на машины
![1-23](./img/Ansible_Playbook_Nginx.png)
### Тестируем сайт `curl -v <публичный IP балансера>:80` 
![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/0ef5b0b7-ac30-4bd2-bff6-845771ce7926)
![alt-text](https://github.com/chichnikita/DiplomNetology/blob/main/img/gif/Site.gif)
### Проверяем корректность работы balancer
![1-20](./img/balancer_logs.png)

## Мониторинг
### Устанавливаем zabbix-server на машину
![1-20](./img/Ansible_Playbook_Zabbix-server_1.png)
![1-20](./img/Ansible_Playbook_Zabbix-server_2.png)

### Установиваем Zabbix Agent на web-server1, web-server2 и настраиваем агенты на отправление метрик в Zabbix.
![1-20](./img/Ansible_Playbook_Zabbix-agent_1.png)
![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/64533ebb-e9c1-494c-81e0-daf130a7fc2f)

### Настраиваем дешборды с отображением метрик, минимальный набор — по принципу USE (Utilization, Saturation, Errors) для CPU, RAM, диски, сеть, http запросов к веб-серверам.

## Логи
### Устанавливаем elasticsearch на сервера web-server1, web-server2
![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/435a77d8-3024-49b2-b2f1-8f359728677f)
### Устанавливаем filebeat
![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/cb055c34-172f-4635-bcbf-8781cbea9e22)

### Устанавливаем kibana
![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/22c891e0-020b-42e6-8105-c75485e803f2)
   
## Резервное копирование
### Создаем snapshot

![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/0d3eae1e-4043-48c5-a3c0-41c300518cce)
