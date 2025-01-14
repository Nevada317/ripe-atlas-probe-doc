# CentOS 8: Установка предварительно собранного ПО из RPM-пакета

Если вы хотите установить новую виртуальную машину с CentOS 7 для размещения вашего зонда:

* Установите CentOS 7 (например используя [VirtualBox](https://www.virtualbox.org/) или [Parallels](https://www.parallels.com/)), в руководствуясь [иструкцией по установке CentOS](https://docs.centos.org/en-US/centos/install-guide/).

* Настраивая систему, переключите сетевой адаптер в режим моста (bridge mode), работал IPv6. По умолчанию обычно используется режим совмещённого доступа (shared), который обеспечивает только IPv4 NAT.

RIPE NCC поддерживает бинарные пакеты RPM дял CentOS 7 (`x86_64`). Для того, чтобы добавить репозиторий к себе в систему, выполните следующие шаги:

1. Скачайте пакет, который добавляет репозиторий с программным обеспечением для зонда:

    ```
    curl -O 'https://ftp.ripe.net/ripe/atlas/software-probe/centos8/noarch/ripe-atlas-repo-1-2.el8.noarch.rpm'
    ```

2. Проверьте хеш-сумму пакета:

    ```
    sha256sum ripe-atlas-repo-1-2.el8.noarch.rpm
    ```

    Хеш должен совпасть с указаннм:

    ```
    cfb433f54395f5d2ac0d29e806f19f1b854d33f02c256087586e50e49003929c
    ```

3. Установите RPM:

    ```
    yum install ripe-atlas-repo-1-2.el8.noarch.rpm
    ```

    В процессе установки, отвечайте Да (`д`/`y`) на возникающие вопросы.


4. Теперь установите программное обеспечение для зонда:

    ```
    yum install atlasswprobe
    ```

5. Подтвердите (д) импорт ключа GPG с отпечатком `afbe 52eb 213a 90ef c72a 39dd 1b48 2af7 830d 38d5`

6. Подтвердите (д) установку пакета `atlasswprobe`. Возможно при этом также потребуется принять ключ подписи CentOS.

7. При установке, программное обеспечение зонда создаёт новую пару ключей SSH
   (публичный и секретный), которые будут использоваться для подключения зонда
   к инфраструктуре RIPE Atlas.
   Вы должны указать **публичный** ключ в процессе
   [регистрации зонда](https://atlas.ripe.net/apply/swprobe/)
   в системе RIPE Atlas.
   Этот ключ после установки программного
   обеспечения будет находиться в файле `/var/atlas-probe/etc/probe_key.pub`.
