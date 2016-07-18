Bem vindo a documentação do Mink!
=================================

Uma das partes mais importantes da web é o navegador. Navegador é a janela através
dela usuários web interagem com aplicações web e outros usuários. Usuários estão 
sempre falando com aplicações web através dos navegadores.

Então, a fim de testar se aquela nossa aplicação web se comporta corretamente, 
nós precisamos de uma forma para simular esta interação entre o navegador e a 
aplicação web em nossos testes. Nós precisamos do **Mink**.

O Mink é um navegador open source controlador/emulador para aplicações web, 
escrito em PHP 5.3.

Leia :doc:`de-relance` para aprender mais sobre o Mink e porque você precisa dele.


Instalação
----------

Mink é uma biblioteca php 5.3 que você vai usar dentro de suas suites de teste 
ou projeto. Antes de você começar, garanta que você tem o PHP 5.3.1 ou superior 
instalado.

A forma recomendada para instalar o Mink com todas as suas dependências é através 
do `Composer`_:

.. code-block:: bash

    $ composer require behat/mink

.. note::

    Para instalações locais do composer você precisa dizer a ele algo como isto:
    ``$ php composer.phar require behat/mink`` .
    Neste caso você precisa utilizar uma chamada diferente
    ``php composer.phar`` em todos os lugares ao invés de simplesmente o comando ``composer``.

Tudo será instalado dentro da pasta ``vendor``.
Finalmente, inclua o script auto carregável Composer ao seu projeto:

.. code-block:: php

    require_once 'vendor/autoload.php';

.. note::

    Por padrão, o Mink será instalado sem drivers. A fim de ser capaz de utilizar 
    divers adicionais, você deve instalá-los (através do composer).
    Eixija as dependencias apropriadas:

    - GoutteDriver - ``behat/mink-goutte-driver``
    - Selenium2Driver - ``behat/mink-selenium2-driver``
    - BrowserKitDriver - ``behat/mink-browserkit-driver``
    - ZombieDriver - ``behat/mink-zombie-driver``
    - SeleniumDriver - ``behat/mink-selenium-driver``
    - SahiDriver - ``behat/mink-sahi-driver``
    - WUnitDriver - ``behat/mink-wunit-driver``

    Se você é novato ou simplesmente você não sabe qual escolher, você deverá 
    provavelmente iniciar com o GoutteDriver e o Selenium2Driver (você poderá 
    substituí-lo depois):

Guias
------

Aprenda Mink com as guias de tópicos:

.. toctree::
    :maxdepth: 1

    de-relance
    guides/sessao
    guides/atravessando-paginas
    guides/manipulando-paginas
    guides/interagindo-com-paginas
    guides/drivers
    guides/gerindo-sessoes
    contribuindo

Ferramentas de Teste de Integração
----------------------------------

O mink tem integrações com muitas ferramentas de teste:

- `Behat`_ através da `Behat MinkExtension`_
- `PHPUnit`_ através do `phpunit-mink package`_

.. _Behat: http://behat.org
.. _Behat MinkExtension: https://github.com/Behat/MinkExtension
.. _Composer: https://getcomposer.org
.. _PHPUnit: http://www.phpunit.de
.. _phpunit-mink package: https://github.com/minkphp/phpunit-mink