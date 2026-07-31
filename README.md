# zabbix_hw
## Homework for the "Monitoring" module. Topic: Zabbix.

#

#### Задание
Установите Zabbix Agent на два хоста.
#
Скрины выполнения:

[Дашборд внешнего агента](img/host-dashboard.png)

[Метрики обоих агентов](img/hosts-latest-data.png)

[Хосты подкючены и работают](img/hosts-working.png)

[Статус в консоли заббикс-агента](img/status-zabbix-agent.png)

[Статус в консоли заббикс-сервера](img/status-zabbix-server.png)
#
Скачивание Заббикса отсюда:
	  https://www.zabbix.com/ru/download
#
	  автоматизация установки заббикса:
	  вместо консольных для создания юзера и бд в постгрескл:

	  sudo -u postgres createuser --pwprompt zabbix
	  sudo -u postgres createdb -O zabbix zabbix

	  делаем для автоматизации(123456789 это пароль, ставить нормальный в реальном проекте):
	  su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD '\'123456789\'';"'
	  su - postgres -c 'psql --command "CREATE DATABASE zabbix OWNER zabbix;"'
#
	  автоматизация пункта "Отредактируйте файл
	  /etc/zabbix/zabbix_server.conf
	  DBPassword=password"
	  вместо него можно использовать sed:
	  sed -i 's/# DBPassword=/DBPassword=123456789/g' /etc/zabbix/zabbix_server.conf
#
	  веб-морда заббикса:
	  http://hostIPorDNS/zabbix
	  стартовый логин: Admin
	  стартовый пароль: zabbix
#
	  для Агента изменить конфиг чтобы прописать ему разрешение отвечать нашему заббикс-серверу:
	  sed -i 's/# Server=/Server=158.160.205.159/g' /etc/zabbix/zabbix_agentd.conf

	  рестартовать сервис агента:
	  systemctl restart zabbix-agent
