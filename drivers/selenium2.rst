Selenium2Driver
===============

O Selenium2Driver fornece uma ponte para a ferramenta `Selenium2 (webdriver)`_.
Se você ama o Selenium2, agora você pode usá-lo corretamente fora da caixa também.

Instalação
----------

O Selenium2Driver está disponível através do Composer:

.. code-block:: bash

    $ composer require behat/mink-selenium2-driver

Afim de falar com o servidor do selenium, você deve instalar e confirá-lo 
primeiramente:

1. Faça o Download do Servidor do Selenium do `site do projeto`_.

2. Execute o servidor com o seguinte comando (altere a versão para o número 
   que você baixou):

   .. code-block:: bash

        $ java -jar selenium-server-standalone-2.44.0.jar

.. tip::

    O Selenium2Driver atualmente confia no protocolo WebDriver definido pelo 
    Selenium2. Isto significa que é possível usá-lo em outras implementações 
    do protocolo. Nove, porém, que outras implementações podem ter alguns bugs.

    A suite de testes do driver é executada contra a `implementação Phantom.js`_ 
    mas ainda desencadeia algumas falhas devido os bugs na sua implementação.

Uso
---

É isso aí, agora você pode usar o Selenium2Driver:

.. code-block:: php

    $driver = new \Behat\Mink\Driver\Selenium2Driver('firefox');

.. _implementação Phantom.js: http://phantomjs.org/
.. _site do projeto: http://seleniumhq.org/download/
.. _Selenium2 (webdriver): http://seleniumhq.org/
