SeleniumDriver
==============

SeleniumDriver fornece uma ponte para a famosa ferramenta `Selenium`_. 
Se você precisar do legado Selenium, você pode usá-lo direito fora da 
caixa nas suas suites de test Mink.

.. caution::

    O protocolo SeleniumRC usado por este driver está obsoleto e não 
    será suportado por todas as funcionalidades do Mink. Por esta razão, 
    o SeleniumDriver está obsoleto a favor do :doc:`/drivers/selenium2`, 
    que é baseado no novo protocolo e é mais poderoso.

Instalação
----------

SeleniumDriver está disponível através do Composer:

.. code-block:: bash

    $ composer require behat/mink-selenium-driver

Afim de conversar com o servidor selenium, você deve instalar e configurá-lo 
primeiro:

1. Baixe o Servidor Selenium do `website do projeto`_.

2. Execute o servidor com o seguinte comando (atualize a versão para o número 
   que você baixou):

   .. code-block:: bash

        $ java -jar selenium-server-standalone-2.44.0.jar

Uso
---

É isso aí, agora você pode usar o SeleniumDriver:

.. code-block:: php

    $client = new \Selenium\Client($host, $port);
    $driver = new \Behat\Mink\Driver\SeleniumDriver(
        'firefox', 'base_url', $client
    );

.. _website do projeto: http://seleniumhq.org/download/
.. _Selenium: http://seleniumhq.org/
