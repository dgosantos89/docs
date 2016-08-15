Analisando Páginas
==================

A maioria dos usos do Mink envolverá trabalhar com a página aberta em seu 
navegador. Isto é feito graças ao poderoso Elemento API. Esta API permite 
a análise da página (similar ao DOM em Javascript), :doc:`manipular elementos da página </guides/manipulando-paginas>`
e para :doc:`interegir com eles </guides/interagindo-com-paginas>`, o qual 
será coberto nos próximos capítulos.

DocumentElement e NodeElement
-----------------------------

O Elemento API consiste em 2 classes principais. A instância ``DocumentElement`` 
representa a página a ser exibida no navegador, enquanto a classe ``NodeElement`` 
é usada para representar qualquer elemento dentro da página. Ambas classes 
compartilham um conjunto comum de métodos para analisar a página (definidos em 
``TraversableElement``).

A instância ``DocumentElement`` é acessível através do método ``Session::getPage``:

.. code-block:: php

    $page = $session->getPage();

    // Agora você pode manipular a página.

.. note::

    A instância ``DocumentElement`` representa o nó ``<html>`` no DOM. É equivalente 
    ao ``document.documentElement`` no DOM API do Javascript.

Métodos de Análise
------------------

Elementos tem 2 métodos principais: ``ElementInterface::findAll`` retorna um 
array de instâncias ``NodeElement`` correspondentes ao :ref:`seletor <seletores>` 
fornecido dentro do elemento atual enquanto ``ElementInterface::find`` retorna 
a primeira combinação ou ``null`` quando não há ninguém.

A classe ``TraversableElement`` também provê um grupo de métodos atalho no 
topo do ``find()`` para torná-lo mais fácil de conseguir muitos casos de uso 
em comum:

``ElementInterface::has``
    Checa se um elemento filho combina com um dado seletor, mas sem devolvê-lo.

``TraversableElement::findById``
    Procura um elemento filho com um dado id.

``TraversableElement::findLink``
    Procura um link com um dado texto, title, id ou atributo ``alt``
    (para imagens usadas dentro de links).

``TraversableElement::findButton``
    Procura por um botão com um dado texto, title, id, atributo ``name`` 
    ou um atributo ``alt`` (para imagens usadas dentro de links).

``TraversableElement::findField``
    Procura por um campo (``input``, ``textarea`` ou ``select``) com um dado 
    label, placeholder, id ou atributo ``name``.

.. note::

    Estes atalhos estão retornando um único elemento. Se você precisa encontrar 
    todos correspondentes, você irá precisar usar ``findAll`` com o :ref:`seletor named <seletor-named>`.

Analisando Aninhado
~~~~~~~~~~~~~~~~~~~

Cada método ``find*()`` retornará uma instância ``Behat\Mink\Element\NodeElement`` 
e ``findAll()`` irá retornar um array das tais instâncias. A parte divertida 
é que você pode fazer a mesma velha análise nos tais elementos também:

.. code-block:: php

    $formularioRegistrar = $page->find('css', 'form.registrar');

    if (null === $formularioRegistrar) {
        throw new \Exception('O elemento não foi encontrado');
    }

    // busca algum campo DENTRO do formulário com a class="registrar"
    $campo = $formularioRegistrar->findField('Email');

.. _selectors:

Seletores
---------

Os métodos ``ElementInterface::find`` e ``ElementInterface::findAll`` 
suporta vários tipos de seletores para encontrar elementos.

Seletor CSS
~~~~~~~~~~~

O tipo de seletor ``css``  permite você usar expressões CSS para buscar 
por elementos na página:

.. code-block:: php

    $titulo = $page->find('css', 'h1');

    $iconeBotao = $page->find('css', '.btn > .icon');

Seletor XPath
~~~~~~~~~~~~~

O seletor tipo ``xpath`` permite você usar queries XPath para buscar 
por elementos na página:

.. code-block:: php

    $ancorasSemUrl = $page->findAll('xpath', '//a[not(@href)]');

.. caution::

    Este seletor busca por um elemento dentro do nó atual (que é 
    ``<html>`` para o objeto da página). Isto significa que tentando 
    passar o XPath de um elemento recuperado com ``ElementInterface::getXpath`` 
    não irá funcionar (esta query inclui a query para o nó raiz). Para 
    checar se um objeto elemento ainda existe na página do navegador, 
    use ``ElementInterface::isValid`` como alternativa.

.. _named-selector:

Seletores Named
~~~~~~~~~~~~~~~~~~

Seletores named fornecem um conjunto de queries para necessidades 
comuns. Para condições baseadas no conteúdo dos elementos, o seletor named 
irá tentar encontrar a primeira correspondência exata. No caso de não obter 
uma correspondência exata será então um retorno correspondente parcial.

Para o tipo seletor named, o segundo argumento para o método ``find()`` 
é um array com 2 elementos: o nome da query que irá usar e o valor da busca 
nesta query:

.. code-block:: php

    $valorEscapado = $session->getSelectorsHandler()->xpathLiteral('Go to top');

    $topLink = $page->find('named', array('link', $valorEscapado));

.. caution::

    O seletor named requer um valor escapando como XPath literal. De 
    outra forma a query XPath gerada será inválida.

As seguintes queries são suportadas pelo seletor named:

``id``
    Busca um elemento pelo seu id.
``id_or_name``
    Busca um elemento pelo seu id ou name.
``link``
    Busca um link pelo seu id, title, img alt, rel ou text.
``button``
    Busca um botão pelo seu name, id, text, img alt ou title.
``link_or_button``
    Busca links e botões.
``content``
    Busca um conteúdo especifico da página (texto).
``field``
    Busca um campo no formulário pelo seu id, name, label ou placeholder.
``select``
    Busca um campo select pelo seu id, name ou label.
``checkbox``
    Busca um checkbox pelo seu id, name, ou label.
``radio``
    Busca um radio button pelo seu id, name, ou label.
``file``
    Busca um file input pelo seu id, name, ou label.
``optgroup``
    Busca um optgroup pelo seu label.
``option``
    Busca um option pelo seu content ou value.
``fieldset``
    Busca um fieldset pelo seu id ou legend.
``table``
    Busca uma table pelo seu id ou caption.

Seletor Customizado
~~~~~~~~~~~~~~~~~~~

O Mink permite você registrar seus próprios tipos de seletor através da implementação da ``Behat\Mink\Selector\SelectorInterface``.
Isto deve então ser registrado no ``SelectorsHandler`` que tem registo dos seletores disponíveis.

A forma recomendada para registrar um seletor customizado é fazê-lo quando construir sua ``Session``:

.. code-block:: php

    $selector = new \App\MySelector();

    $handler = new \Behat\Mink\Selector\SelectorsHandler();
    $handler->registerSelector('mine', $selector);

    $driver = // ...

    $session = new \Behat\Mink\Session($driver, $handler);
