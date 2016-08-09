GoutteDriver
============

GoutteDriver fornece uma ponte para o `Goutte`_ headless browser. Goutte 
é um clássico php-puro headless browser, escrito pelo criador do framework 
Symfony Fabien Potencier.

.. note::

    O GoutteDriver estende-se do :doc:`/drivers/browserkit` para consertar 
    um caso extremamente pequeno na implementação Goutte do Browserkit. Ele 
    também é capaz de instanciar o cliente Goutte automaticamente.

Instalação
----------

GoutteDriver é uma biblioteca PHP pura disponibilizada através do Composer:

.. code-block:: bash

    $ composer require behat/mink-goutte-driver

.. note::

    GoutteDriver é compatível em ambos Goutte 1.x o qual confia no `Guzzle 3`_ 
    e Goutte 2.x o qual confia no `Guzzle 4+`_ para a implementação HTTP adjacente.

    O Composer provavelmente irá selecionar o Goutte 2.x por padrão.

Uso
---

Afim de falar com o Goutte, você deverá instanciar um ``Behat\Mink\Driver\GoutteDriver``:

.. code-block:: php

    $driver = new \Behat\Mink\Driver\GoutteDriver();

Também, se você quiser configurar o Goutte com maior precisão, você poderia fazer 
a configuração total na mão:

.. code-block:: php

    $client = new \Goutte\Client();
    // Faça mais configurações para o cliente Goutte

    $driver = new \Behat\Mink\Driver\GoutteDriver($client);

.. _Goutte: https://github.com/FriendsOfPHP/Goutte
.. _Guzzle 3: http://guzzle3.readthedocs.org/en/latest/
.. _Guzzle 4+: http://docs.guzzlephp.org/en/latest/
