ZombieDriver
============

O ZombieDriver fornece uma ponte para o emulador de navegador `Zombie.js`_. 
Zombie.js é um emulador de browser headless, escrito em node.js. Ele suporta 
todas as interações JS :doc:`Selenium </drivers/selenium2>` e :doc:`Sahi </drivers/sahi>` 
funciona quase tão rápido quanto o Goutte faz. Atualmente ele é o melhor dos 
dois mundos, mas ainda limitado a apenas um tipo de navegador (Webkit). Também 
ainda é mais devagar que o Goutte e requerem que o node.js e npm estejam 
instalados no sistema.

Instalação
----------

ZombieDriver está disponível através do Composer:

.. code-block:: bash

    $ composer require behat/mink-zombie-driver

Afim de falar com um servidor zombie.js, você precisa instalar e configurar 
o zombie.js primeiramente:

1. Instale o node.js com as seguintes instruções do site oficial:
   `<http://nodejs.org/>`_.

2. Instale o npm (node package manager) pela seguinte instruções do
   `<http://npmjs.org/>`_.

3. Instale o zombie.js com npm:

    .. code-block:: bash

        $ npm install -g zombie

Depois de instalar npm e zombie.js, você precisará adicionar as bibliotecas do 
npm em seu ``NODE_PATH``.
A forma mais fácil de fazer isto é adicionar:

.. code-block:: bash

    export NODE_PATH="/PATH/TO/NPM/node_modules"

em seu ``.bashrc``.

Uso
---

Depois disto, você estará capaz de usar somente o ZombieDriver sem a instalação 
manual do servidor. O driver irá fazer tudo isto para você automaticamente:

.. code-block:: php

    $driver = new \Behat\Mink\Driver\ZombieDriver(
        new \Behat\Mink\Driver\NodeJS\Server\ZombieServer()
    );

Se você quer mais controle durante a instalação do driver, por exemplo se você 
quer configurar o driver para ser inicializado no servidor em uma porta 
específica, use a versão mais verbosa:

.. code-block:: php

    $driver = new \Behat\Mink\Driver\ZombieDriver(
        new \Behat\Mink\Driver\Zombie\Server($host, $port, $nodeBin, $script)
    );

.. note::

    ``$host`` simplesmente define o host em que o zombie.js será inicializado. 
    Por padrão é ``127.0.0.1``.

    ``$port`` define uma porta zombie.js. A padrão é ``8124``.

    ``$nodeBin`` define o caminho completo do binário do node.js. Por padrão é somente ``node``.

    ``$script`` define um script node.js para inicializar um servidor zombie.js. 
    Se você passar um ``null`` o script padrão será usado. Use está opção cuidadosamente!

.. _Zombie.js: http://zombie.labnotes.org/
