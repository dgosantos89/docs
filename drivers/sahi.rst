SahiDriver
==========

O SahiDriver fornece uma ponte para o controlador de navegador `Sahi`_. 
Sahi é um novo controlador de navegador JS, que substituiu rapidamente 
a velha suite de testes Selenium. É tão mais fácil configurar e usar do 
que o Selenium classico. Ele tem um instalador GUI para cada sistema 
operacional lá fora e é capaz de controlar cada sistema navegador através 
de um servidor de proxy especial empacotado.

Instalação
------------

SahiDriver está disponível através do Composer:

.. code-block:: bash

    $ composer require behat/mink-sahi-driver

Afim de falar com um navegador real através do Sahi, você deve instalar e
configurar o Sahi primeiramente:

1. Faça o download e execute o jar do Sahi do `site do projeto Sahi`_ e 
   o execute. Ele irá executar o instalador, que irá lhe guiar através do 
   processo de instalação.

2. Execute o proxy Sahi antes das suas suites de teste (você pode iniciar 
   este proxy durante a inicialização do sistema):

    .. code-block:: bash

        cd $YOUR_PATH_TO_SAHI/bin
        ./sahi.sh

Uso
---

Depois de instalar o Sahi e executar o servidor de proxy Sahi, você estará 
hábil a o controlar com ``Behat\Mink\Driver\SahiDriver``:

.. code-block:: php

    $driver = new \Behat\Mink\Driver\SahiDriver('firefox');

.. note::

    Aviso, que o primeiro argumento do ``SahiDriver`` sempre será o nome do 
    navegador, `suportado pelo Sahi`_.

Se você quiser maior controle durante a inicialização do driver, por exemplo, 
se você quiser configurar o driver para falar com um proxy em outra máquina, 
utilize a versão mais verbosa com um segundo argumento cliente:

.. code-block:: php

    $driver = new \Behat\Mink\Driver\SahiDriver(
        'firefox',
        new \Behat\SahiClient\Client(
            new \Behat\SahiClient\Connection($sid, $host, $port)
        )
    );

.. note::

    ``$sid`` é uma sessão ID do Sahi. Ele é uma string única, usada pelo driver 
    e o proxy Sahi afim de possibilitar a conversa com cada outro. Vôcê deve 
    preencher isto com ``null`` se você quiser que o Sahi inicie seu navegador 
    automaticamente ou com alguma string única se você quiser controlar um 
    navegador já inicializado.

    ``$host`` simplesmente define o host no qual o Sahi é iniciado. Por padrão 
    é o ``localhost``.


    ``$port`` define a porta do proxy Sahi. O padrão inicial é ``9999``.

.. _Sahi: http://sahi.co.in/w/
.. _site do projeto Sahi: http://sourceforge.net/projects/sahi/files/
.. _suportado pelo Sahi: http://sahi.co.in/w/browser-types-xml
