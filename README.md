#  Дипломная работа по профессии «Системный администратор»

Техническое задание : [Диплом sys-22](https://github.com/chichnikita/DiplomNetology/blob/main/Read_tx.md)  
[Информация по подключениям к серверам ](https://github.com/chichnikita/DiplomNetology/blob/main/info.md)

## Инфраструктура
Для развёртки инфраструктуры использую Terraform и Ansible.
 * Terraform - смотрите terraform/main.ft и все прилагающие к нему файлы
 * Описывать метод подключения terraform к yandex cloud не буду - все было в лекциях, вебинарах и домашних заданиях, там все очень грамматно и четко показывали и объясняли.

<details> 

Использовал следующий принцип работы, создал один каталог bastion-new -  на нём сервер terraform. При развертывание terraform, вся инфраструктура разворачивается в другом катологе diplom-new.

   ![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/95ea0227-5d94-4ee8-8567-de544738de46)


## Разворачиваем инфраструктуру используя Terraform 
   ![alt text](https://github.com/chichnikita/DiplomNetology/blob/main/img/Terraform_Init_Validate_Fmt.png?raw=true)
   
   ![alt text](https://github.com/chichnikita/DiplomNetology/blob/main/img/Terraform_Apply.png?raw=true)
   
   ![alt text](https://github.com/chichnikita/DiplomNetology/blob/main/img/Terraform_Apply_End.png?raw=true)
   ![alt-text](https://github.com/chichnikita/DiplomNetology/blob/main/img/gif/Terraform_Apply.gif)
   
Использовал минимальные конфигурации ВМ:2 ядра 20% Intel ice lake, 2-4Гб памяти, 10hdd, прерываемая.
## Проверяем параметры созданых виртуальных машин
  ![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/48b1670d-15ec-480b-a969-7021ba337da8)



Виртуальная машина github - это личный сервер, к проекту он не имеет никакого отношения :) 

</details>

## Сайт
### Проверяем созданую Target Group

<details> 
   
![1-20](./img/tg.png)

</details> 
   
### HTTP router

<details> 
   
![1-21](./img/router.png)

</details> 
   
### Backend Group

<details> 
   

![1-22](./img/bg.png)

</details> 

### Balancer

<details> 

![1-22](./img/Balancer.png)

</details> 

### Проверяем созданую группу безопасности

<details> 

![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/be668b36-a6c3-4ccd-91e7-6e4d1727708e)


</details> 

### С помощью Ansible проверяем доступность созданых виртуальных машин

<details> 

![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/eba01c45-06f1-451e-ba52-f4c984c88e55)


</details> 


### Для ansible inventory использовал fqdn имена виртуальных машин в зоне ".ru-central1.internal"  

<details> 

![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/ac020a07-b8c4-411d-897c-bf080cabcdef)


</details> 

### Устанавливаем Nginx на машины

<details> 

![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/45f4a580-3423-43d3-95a5-7320fe0b6d28)


</details> 

### Тестируем сайт `curl -v <публичный IP балансера>:80` 

[Информация по подключениям к серверам ](https://github.com/chichnikita/DiplomNetology/blob/main/info.md)

<details> 
   
![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/0ef5b0b7-ac30-4bd2-bff6-845771ce7926)


</details> 



![alt-text](https://github.com/chichnikita/DiplomNetology/blob/main/img/gif/Site.gif)
### Проверяем корректность работы balancer

<details> 

![1-20](./img/balancer_logs.png)

</details> 

## Мониторинг
### Устанавливаем zabbix-server на машину 
[Информация по подключениям к серверам ](https://github.com/chichnikita/DiplomNetology/blob/main/info.md)
<details> 

![1-20](./img/Ansible_Playbook_Zabbix-server_1.png)
![1-20](./img/Ansible_Playbook_Zabbix-server_2.png)


</details> 


### Установиваем Zabbix Agent на web-server1, web-server2 и настраиваем агенты на отправление метрик в Zabbix.

<details> 

![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/17853cec-65be-41a4-937e-e2e597c0e704)

![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/64533ebb-e9c1-494c-81e0-daf130a7fc2f)

</details> 

### Настраиваем дешборды с отображением метрик, минимальный набор — по принципу USE (Utilization, Saturation, Errors) для CPU, RAM, диски, сеть, http запросов к веб-серверам.

## Логи
### Устанавливаем elasticsearch на сервера web-server1, web-server2

<details> 
   
![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/435a77d8-3024-49b2-b2f1-8f359728677f)

</details> 
   
### Устанавливаем filebeat

<details> 

![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/cb055c34-172f-4635-bcbf-8781cbea9e22)

</details> 

### Устанавливаем kibana

<details>
   
![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/22c891e0-020b-42e6-8105-c75485e803f2)

</details> 
   
## Резервное копирование
### Создаем snapshot

<details> 

![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/0d3eae1e-4043-48c5-a3c0-41c300518cce)

</details> 
  
## Спасибо большое за данный курс и возможность научиться много новому, после защиты диплома собираюсь купить и пройти другие курсы, всем советую!
