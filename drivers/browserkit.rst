BrowserKitDriver
================

BrowserKitDriver provê uma ponte para o componente `Symfony BrowserKit`_.
BrowserKit é um emulador de navegador fornecido pelo `Symfony project`_.

Instalação
----------

BrowserKitDriver é uma biblioteca PHP pura disponível através do Composer:

.. code-block:: bash

    $ composer require behat/mink-browserkit-driver

.. note::

    O componente BrowserKit somente provê uma implementação abstrata. As 
    implementações atuais são fornecidas por outros projetos, como `Goutte`_ 
    ou o componente `Symfony HttpKernel`_.

    Se você está usando Goutte, você deve usar o especial :doc:`/drivers/goutte` 
    que garante completa compatibilidade com o Goutte devido um caso extremo no Goutte.

Uso
---

Afim de falar conversar com o BrowserKit, você deve instanciar um ``Behat\Mink\Driver\BrowserKitDriver``:

.. code-block:: php

    $browserkitClient = // ...

    $driver = new \Behat\Mink\Driver\BrowserKitDriver($browserkitClient);

.. _Goutte: https://github.com/FriendsOfPHP/Goutte
.. _Symfony BrowserKit: http://symfony.com/components/BrowserKit
.. _Symfony HttpKernel: http://symfony.com/components/HttpKernel
.. _Symfony project: http://symfony.com
