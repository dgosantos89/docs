Controlando o Navegador
=======================

No Mink, o ponto de entrada do navegador é chamado de sessão. Pense nisso 
como sendo a janela do navegador (alguns drivers até deixam você alternar 
guias!).

Primeiro, inicie sua sessão (é como abrir a guia do seu navegador). Nada pode 
ser feito com isto antes de iniciá-lo.

.. code-block:: php

    // Escolha um driver Mink. Veja mais sobre isto nos capítulos seguintes.
    $driver = new \Behat\Mink\Driver\GoutteDriver();

    $session = new \Behat\Mink\Session($driver);

    // inicia a sessão
    $session->start();

.. note::

    O primeiro argumento do construtor da sessão é um objeto driver. Drivers 
    são a forma de abstração que as camadas Mink trabalham. Você irá descobrir 
    mais sobre os drivers disponíveis em um :doc:`capitulo posterior </guides/drivers>`.

.. caution::

    Apesar do Mink fazer o seu melhor para remover as diferenças entre os 
    diferentes drivers, cada driver tem funcionalidades e deficiências 
    diferentes. Veja :ref:`driver-feature-support` para ver cada funcionalidade 
    são suportadas sobre cada driver.

Interação Básica no Navegador
-----------------------------

Agora que sua sessão está iniciada, você irá querer abrir uma página com ele. 
Apenas depois de começar, a sessão não está em uma página qualquer (em um navegador 
real, você estaria na página ``about:blank``), e chamando qualquer outra ação 
é provável que falhe.

.. code-block:: php

    $session->visit('http://meu_projeto.dev/alguma_pagina.php');

.. note::

    Mink é principalmente projetado para ser usado para testar websites. 
    Para que você possa navegar e testar páginas de erro, o método 
    ``Session:visit`` não considera códigos de status de erro como inválida. 
    Ele *não* irá lançar uma exceção neste caso. Você irá precisar checar 
    o código do status (ou certo texto na página) para saber se a resposta 
    teve sucesso ou não.

Interagindo com a Página
------------------------

A sessão dá acesso a página através do método ``Session::getPage``. 
Isto lhe permite :doc:`analisar a página </guides/analisando-paginas>` e 
:doc:`interagir </guides/interagindo-com-paginas>` com elas. Os próximos 
capítulos cobrem a página API com profundidade. A maioria do que você vai 
fazer com Mink usará este objeto, mas você pode continuar lendo para saber 
mais sobre Sessão.

Usando o Histórico do Navegador
-------------------------------

A sessão lhe da acesso ao histórico do navegador:

.. code-block:: php

    // obter a URL da página atual:
    echo $session->getCurrentUrl();

    // usar controles de histórico:
    $session->reload();
    $session->back();
    $session->forward();

Gerenciamento de Cookie
-----------------------

A sessão pode manipular cookies disponíveis no navegador.

.. code-block:: php

    // definir cookie:
    $session->setCookie('cookie nome', 'valor');

    // obter cookie:
    echo $session->getCookie('cookie nome');

    // deletar cookie:
    $session->setCookie('cookie nome', null);

.. note::

    Com drivers que usam o JavaScript para controlar o navegador - como Sahi - 
    que pode ser restringido a acessar/definir tudo, mas `Cookies HttpOnly`_.

Código de Status de Recuperação
-------------------------------

A sessão lhe permite recuperar o código HTTP do status da resposta:

.. code-block:: php

    echo $session->getStatusCode();

Gerenciamento de Headers
------------------------

A sessão lhe permite manipular request de headers e acessar a resposta dos headers:

.. code-block:: php

    // definindo linguagem do navegador:
    $session->setRequestHeader('Accept-Language', 'fr');

    // recuperação da resposta do headers:
    print_r($session->getResponseHeaders());

.. note::

    A manipulação de headers somente é suportada em drivers headless (como 
    o Goutte, por exemplo). Controladores de navegadores (como o Selenium2, 
    por exemplo) não podem acessar aquela informação.

Autenticação HTTP
-----------------

A sessão tem um método  especial para atuar na autenticação básica de HTTP:

.. code-block:: php

    $session->setBasicAuth($user, $password);

O método pode também ser usado para reiniciar uma autenticação prévia:

.. code-block:: php

    $session->setBasicAuth(false);

.. note::

    Autenticação HTTP automática somente é suportada em drivers headless. 
    Porque autenticação HTTP nos navegadores exigem atuação manual do usuário, 
    que não pode ser feita remotamente pelos controladores de navegador.

Avaliação do Javascript
-----------------------

A sessão lhe permite executar ou avaliar Javascript.

.. code-block:: php

    // Executar JS
    $session->executeScript('document.body.firstChild.innerHTML = "";');

    // analisar expressão JS:
    echo $session->evaluateScript(
        "return 'algo a partir do navegador';"
    );

.. note::

    A diferença entre estes métodos é que ``Session::evaluateScript`` retorna 
    o resultado desta expressão. Quando você não precisa obter o valor do 
    retorno, usar ``Session::executeScript`` é melhor.

Você pode também esperar até uma determinada expressão JS retornar um valor 
booleano verdadeiro ou o tempo limite ser atingido:

.. code-block:: php

    // esperar por N milissegundos ou
    // até a expressão JS tornar-se verdadeira:
    $session->wait(
        5000,
        "$('.suggestions-results').children().length"
    );

.. note::

    O método ``Session::wait`` retorna ``verdadeiro`` quando a avaliação retorna 
    verdadeiro. Ele irá retornar ``falso`` quando o timeout é alcançado.

Repondo a Sessão
----------------

O objetivo primário para o Mink é prover um navegação na WEB API única 
consistente para teste de aceite. Mas uma parte muito importante no teste 
é o isolamento.

O Mink provê dois métodos muito úteis para isolar testes, que podem ser usados 
em seus métodos de teste ``destruir``:

.. code-block:: php

    // soft-reset:
    $session->reset();

    // hard-reset:
    $session->stop();
    // ou se você quiser iniciar novamente ao mesmo tempo
    $session->restart();

Parar a sessão é a melhor maneira de reiniciar a sessão ao estado inicial. 
Ele irá fechar o seu navegador inteiramente. Para usar a sessão novamente, 
você precisa iniciar a sessão antes de qualquer outra ação. O atalho 
``Session::restart`` permite você fazer estas 2 chamadas em uma única.

A desvantagem de fechar o navegador e iniciá-lo novamente é que leva tempo. 
Em muitos casos, um nível mais baixo de isolamento é o suficiente a favor de 
uma reinicialização rápida. O método ``Session::reset`` cobre este caso de uso. 
Ele irá tentar limpar os cookies e reiniciar o request de headers e o histórico 
do navegador ao limite das possibilidades do driver.

Levando tudo isto em conta, por padrão é recomendado usar ``Session::reset()`` 
e chamar ``Session::stop()`` quando você realmente precisar de isolamento completo.

.. _Cookies HttpOnly: http://en.wikipedia.org/wiki/HTTP_cookie#HttpOnly_cookie
