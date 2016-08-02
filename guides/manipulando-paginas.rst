Manipulando Páginas
===================

Uma vez que você :doc:`pegue um elemento da página </guides/examinando-paginas>, 
você vai querer manipulá-lo. Você pode também interagir com a página, que é 
coberta no :doc:`próximo capitulo </guides/interagindo-com-paginas>`.

Obtendo o nome da tag
---------------------

O método ``NodeElement::getTagName`` permite você a obter o nome da tag do 
elemento. Este nome da tag é sempre retornado em letras minúsculas.

.. code-block:: php

    $el = $page->find('css', '.something');

    // obter o nome da tag:
    echo $el->getTagName(); // exibe 'a'

Acessando atributos HTML
------------------------

A classe ``NodeElement`` lhe dá acesso aos atributos HTML do elemento.

``NodeElement::hasAttribute``
    Verifica se o elemento tem um determinado atributo.

``NodeElement::getAttribute``
    Obtém o valor de um atributo.

``NodeElement::hasClass``
    Verifica se o elemento tem uma dada classe (convenientemente envolvido em 
    torno de ``getAttribute('class')``).

.. code-block:: php

    $el = $page->find('css', '.something');

    if ($el->hasAttribute('href')) {
        echo $el->getAttribute('href');
    } else {
        echo 'Esta âncora não é um link. Ela não tem um href.';
    }

Elemento de Conteúdo e Texto
----------------------------

A classe ``Element`` provê acesso ao conteúdo dos elementos.

``Element::getHtml``
    Obtém o HTML interno do elemento, por exemplo todos os filhos do elemento.

``Element::getOuterHtml``
    Obtém o HTML exterior do elemento, por exemplo incluindo o próprio elemento.

``Element::getText``
    Obtém o texto do elemento.

.. note::

    ``getText()`` irá retirar tags e caracteres não impressos fora da resposta, 
    incluindo linhas novas. Então ele basicamente retorna o texto, que o usuário 
    vê na página.

Verificando a visibilidade de um Elemento
-----------------------------------------

O método ``NodeElement::isVisible`` permite checar se o elemento está visível.

Acessando o estado do formulário
--------------------------------

A classe ``NodeElement`` permite o acesso ao estado de elementos do formulário:

``NodeElement::getValue``
    Obtém o valor do elemento. Veja :ref:`interagindo-com-formularios`.

``NodeElement::isChecked``
    Verifica se o checkbox ou o radio button está checado.

``NodeElement::isSelected``
    Verifica se o elemento ``<option>`` está selecionado.

Métodos de atalho
~~~~~~~~~~~~~~~~~

A classe ``TraversableElement`` provê uns poucos métodos de atalho permitindo a 
busca de um elemento filho na página e checar o estado dele imediatamente:

``TraversableElement::hasCheckedField``
    Olha para uma checkbox (veja findField) e checa se ela está checada.

``TraversableElement::hasUncheckedField``
    Olha para um checkbox (veja findField) e checa se ele não está checado.
