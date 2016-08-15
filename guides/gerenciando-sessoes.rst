Gerenciando Sessões
===================

Apesar do :doc:`objeto de sessão </guides/sessao>` já estar utilizável o suficiente, 
não é tão fácil escrever um código multissessão (multidriver/multinavegador). Sim, 
você ouviu direito, com o Mink você pode manipular múltiplos emuladores de 
navegador simultaneamente com uma única API consistente:

.. code-block:: php

    // inicialização de sessões
    $sessao1 = new \Behat\Mink\Session($driver1);
    $sessao2 = new \Behat\Mink\Session($driver2);

    // começa sessões
    $sessao1->start();
    $sessao2->start();

    $sessao1->visit('http://my_project.dev/chat.php');
    $sessao2->visit('http://my_project.dev/chat.php');

.. caution::

    O estado de uma sessão é gerenciado atualmente pelo driver. Isto significa 
    que cada sessão precisa usar uma instância diferente de driver.

Não é legal? Mas o Mink torna isto mais frio:

.. code-block:: php

    $mink = new \Behat\Mink\Mink();
    $mink->registerSession('goutte', $goutteSession);
    $mink->registerSession('sahi', $sahiSession);
    $mink->setDefaultSessionName('goutte');

Com tal configuração, você pode falar com suas sessões pelo nome através de 
um único objeto contêiner:

.. code-block:: php

    $mink->getSession('goutte')->visit('http://my_project.dev/chat.php');
    $mink->getSession('sahi')->visit('http://my_project.dev/chat.php');

.. note::

    O Mink sempre irá iniciar suas sessões ociosas quando necessário (na primeira 
    chamada ``getSession()``). Então, o navegador não será inicial até que você 
    realmente precise dele!

Ou você até pode omitir o nome da sessão em casos padrão:

.. code-block:: php

    $mink->getSession()->visit('http://my_project.dev/chat.php');

Esta chamada é possível graças ao ``$mink->setDefaultSessionName('goutte')`` 
configurado previamente. Nós criamos a sessão padrão, que seria devolvida na 
chamada sem argumentos ``getSession()``.

.. tip::

    A classe ``Behat\Mink\Mink`` também provê uma forma fácil de redefinir ou 
    reiniciar suas sessões iniciadas (e somente iniciadas):

    .. code-block:: php

        // redefine sessões iniciadas
        $mink->resetSessions();

        // reinicia sessões iniciadas
        $mink->restartSessions();