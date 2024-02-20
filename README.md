#  Дипломная работа по профессии «Системный администратор»

Техническое задание :
[Диплом sys-22](https://github.com/chichnikita/DiplomNetology/blob/main/Read_tx.md)

## Инфраструктура
Для развёртки инфраструктуры использую Terraform и Ansible.
 * Terraform - смотрите terraform/main.ft и все прилагающие к нему файлы
 * Описывать метод подключения terraform к yandex cloud не буду - все было в лекциях, вебинарах и домашних заданиях, там все очень грамматно и четко показывали и объясняли.


Использовал следующий принцип работы, создал два каталога, на одном стоит сервер terraform, на другом разваричиваются сервера из terraform.

   ![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/95ea0227-5d94-4ee8-8567-de544738de46)

Отдельно я создал сервер bastion-host он ничем не отличается от bastion-host1. Это была временна необходимость, так как при использовании команды terraform destcroy - удалялся сервер с bastion-host1(где лежит весь ansible).
Для того, что каждый раз не перекидывать файлы и заново устаналивать ansible и я поступил таким образом.

   ![image](https://github.com/chichnikita/DiplomNetology/assets/120582480/283d0070-4b4c-4640-adba-82964b9b4271)


   ![alt text](https://github.com/chichnikita/DiplomNetology/blob/main/img/Terraform_Init_Validate_Fmt.png?raw=true)
   
   ![alt text](https://github.com/chichnikita/DiplomNetology/blob/main/img/Terraform_Apply.png?raw=true)
   
   ![alt text](https://github.com/chichnikita/DiplomNetology/blob/main/img/Terraform_Apply_End.png?raw=true)
   
Использовал минимальные конфигурации ВМ:2 ядра 20% Intel ice lake, 2-4Гб памяти, 10hdd, прерываемая.

