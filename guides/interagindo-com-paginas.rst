Interagindo com Páginas
=======================

A maioria dos usos de Mink envolverá trabalhar com páginas abertas em seu navegador.
O elemento Mink API permite você interagir com elementos da página.

Interagindo com Links e Botões
------------------------------

Os métodos ``NodeElement::click`` e ``NodeElement::press`` permitem você clicar 
nos links e apertar os botões na página.

.. note::

    Estes métodos atualmente são equivalentes internamente (pressionar um botão
    envolve clicá-lo). Tento ambos os métodos permitindo manter o código mais legível.

.. _interagindo-com-formularios:

Interagindo com formulários
---------------------------

A classe ``NodeElement`` tem um conjunto de métodos permitindo interagir 
com formulários:

``NodeElement::getValue``
    pega o valor de um campo do formulário. O valor depende do tipo do campo:

    - o valor da opção selecionada para caixas de seleção individuais (ou 
    ``null`` quando nenhuma é selecionada);
    - um array dos valores das opções selecionadas para multiplas caixas de seleção;
    - o valor do campo checkbox quando checado, ou ``null`` quando não checado;
    - o valor do radio button selecionado no grupo de radio para radio buttons;
    - o valor do campo para campos de texto e textareas;
    - um valor indefinido para campos de arquivos (devido as limitações do navegador).

``NodeElement::setValue``
    coloca o valor de um campo do formulário

    - para um campo de arquivo, deveria ser o caminho para o arquivo;
    - para um checkbox, deveria ser um booleano indicando se está checado;
    - para outros campos, deveria corresponder o comportamento de ``getValue``.

``NodeElement::isChecked``
    informa se um radio button ou um checkbox está checado.

``NodeElement::isSelected``
    informa se um elemento ``<option>`` está selecionado.

``NodeElement::check``
    checa um campo checkbox.

``NodeElement::uncheck``
    descheca um campo checkbox.

``NodeElement::selectOption``
    seleciona uma opção em uma caixa de seleção ou em um radio group.

``NodeElement::attachFile``
    anexa um arquivo em uma em uma entrada de arquivo.

``NodeElement::submit``
    submete o formulário.

Interagindo com o mouse
-----------------------

A classe ``NodeElement`` oferece um conjunto de métodos que permitem interagir 
com o mouse:

``NodeElement::click``
    executa um clique no elemento.

``NodeElement::doubleClick``
    executa um clique duplo no elemento.

``NodeElement::rightClick``
    executa um clique com o botão direito no elemento.

``NodeElement::mouseOver``
    move o mouse para cima do elemento.

Interagindo com o teclado
-------------------------

O mink permite você interagir com o teclado graças aos métodos ``NodeElement::keyDown``,
``NodeElement::keyPress`` e ``NodeElement::keyUp``.

Manipulando o Foco
------------------

A classe ``NodeElement`` permite você dar e remover o foco em um elemento 
graças aos métodos ``NodeElement::focus`` e ``NodeElement::blur``.

Clica e arrasta
---------------

Mink provê o clica e arrasta de um elemento para outro:

.. code-block:: php

    $arrastado = $page->find(...);
    $alvo = $page->find(...);

    $arrastado->dragTo($alvo);

Métodos de atalho
-----------------

A classe ``TraversableElement`` provê alguns poucos métodos de atalho 
permitindo procurar um elemento filho na página e executar uma ação imediatamente:

``TraversableElement::clickLink``
    Olha para um link (veja findLink) e clica nele.

``TraversableElement::pressButton``
    Olha para um botão (veja findButton) e o pressiona.

``TraversableElement::fillField``
    Olha para um campo (veja findField) e coloca um valor nele.

``TraversableElement::checkField``
    Olha para um checkbox (veja findField) e checa ele.

``TraversableElement::uncheckField``
    Olha para um checkbox (veja findField) e descheca ele.

``TraversableElement::selectFieldOption``
    Olha para um select ou radio group (veja findField) e seleciona uma opção.

``TraversableElement::attachFileToField``
    Olha para um campo de arquivo (veja findField) e anexa um arquivo a ele.

.. note::

    Todos estes métodos de atalho lançam uma ``ElementNotFoundException``
    no caso do elemento filho não ser encontrado.