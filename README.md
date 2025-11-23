# adm_training_task20
<h1 align="center">Занятие 20. Настройка PXE сервера для автоматической установки</h1>
<ol>
<li><span style="font-weight: 300;"> Настроить загрузку по сети дистрибутива Ubuntu 24</span></li>
<li><span style="font-weight: 300;"> Установка должна проходить из HTTP-репозитория.</span></li>
<li><span style="font-weight: 300;"> Настроить автоматическую установку c помощью файла user-data</span></li>
</ol>
<h3 class="western"><a name="_heading=h.df570rpzx1qg"></a><span style="font-family: Roboto, serif;"><span style="font-size: small;">Используемые ОС</span></span></h3>
<p style="line-height: 108%; margin-bottom: 0.28cm;" align="justify"><span style="font-family: Roboto, serif;">Хостовая ОС Ubuntu 24.04 Desktop с установленным Vagrant 2.3.5. VirtualBox версия 7.0.16_Ubuntu r162802</span></span></p>
<h3 class="western"><span style="font-family: Roboto, serif;"><span style="font-size: small;">Выполнение</span></span></h3>
<p>******************************</p>
<p>Ввиду невозможности в нынешних реалиях воспользоваться стандартными репозиториями Vagrant (в РФ они сейчас не доступны), предложено обходное решение. Использован репозиторий, развернутый на&nbsp;<a href="https://vagrant.elab.pro/" rel="nofollow">https://vagrant.elab.pro/</a></p>
<p>Так как официальный пакет последней версии Vagrant также не доступен для скачивания, пакет взят оттуда же. Версия 2.3.5.</p>
<img width="411" height="88" alt="image" src="https://github.com/user-attachments/assets/7591c684-f543-4bf6-bfa8-3706a7648c97" />
<p>&nbsp;</p>
<p>Для подключения репозитория надо добавить в Vagrant-файл строку:</p>
<p><code>ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'</code></p>
<p>И изменить box_name и box_version (как в репозитории, если туда зайти).</p>
<img width="480" height="306" alt="image" src="https://github.com/user-attachments/assets/c34c2b46-a072-4edd-8ae6-6f0c8d26cde8" />
<p>******************************</p>
<p><strong>1) Разворот хостов и настройка загрузки по сети</strong></p>
<p><span style="font-weight: 300;">Подготовим в каталоге <strong>~/task20</strong> Vagrantfile, в котором будут описаны 2 виртуальные машины:</span></p>
<ul>
<li><span style="font-weight: 300;"> pxeserver (сервер, к которому будут обращаться клиенты для установки ОС)</span></li>
<li><span style="font-weight: 300;"> pxeclient (клиент, на котором будет проводиться установка)</span></li>
</ul>
<p><span style="font-weight: 300;">Vagrantfile взят из методички и изменен в соответствии с обходным решением. Файл прикладываю сюда.</span></p>
<img width="862" height="955" alt="image" src="https://github.com/user-attachments/assets/294aedc4-a890-4028-8236-8bb8584c5112" />
<p>&nbsp;</p>
<p><span style="font-weight: 300;">Данный Vagrantfile развернёт сервер pxeserver, настроит его через Ansible, и далее развернёт клиента pxeclient, который попробует загрузиться через pxe.</span></p>
<p><span style="font-weight: 300;">В Vagrantfile сразу добавлен запуск Ansible-плейбука provision.yaml для настройки сервера. Плейбук со всеми необходимыми файлами находится в каталоге <strong>~/task20/ansible</strong>, файлы прикладываю сюда же.</span></p>



<p><span style="font-weight: 300;">После внесения всех изменений запускаем наш стенд с помощью команды <code>vagrant up</code>.</p>
