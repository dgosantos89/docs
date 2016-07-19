Drivers
=======

Como é que o Mink fornece uma API consistente para vários tipos de bibliotecas 
de navegadores diferentes, frequentemente escritas em diferentes linguagens? 
Através dos drivers! Um driver Mink é uma classe simples, que implementa 
``Behat\Mink\Driver\DriverInterface``. Esta interface descreve metodos pontes 
entre o Mink e os emuladores de navegadores reais. Ele não sabe nada sobre como 
inicar/parar ou atravessar página nesse emulador de navegador em particular. Ele 
somente sabe que método do driver que deve chamar para fazer isso.

O Mink vem com seis drivers fora da caixa:

.. toctree::
    :maxdepth: 1

    /drivers/goutte
    /drivers/browserkit
    /drivers/selenium2
    /drivers/zombie
    /drivers/sahi
    /drivers/selenium

.. _driver-feature-support:

Suporte a recursos do driver
----------------------------

Apesar do Mink faça o seu melhor em remover as diferenças entre navegador e 
diferentes emuladores de navegador, ele não pode fazer muito em alguns casos. 
Por exemplo, BrowserKitDriver não avalia JavaScript e Slenium2Driver não consegue 
pegar código dos status das respostas. Nestes casos, o driver sempre irá lançar 
uma ``Behat\Mink\Exception\UnsupportedDriverActionException`` exceção.

=================================  =================  =========  ======  ========  ====
Funcionalidade                     BrowserKit/Goutte  Selenium2  Zombie  Selenium  Sahi
=================================  =================  =========  ======  ========  ====
Atravessar páginas                 Sim                Sim        Sim     Sim       Sim
Manipular Formulários              Sim                Sim        Sim     Sim       Sim
Autenticação Básica HTTP           Sim                Não        Sim     Não       Não
Gestão de janelas                  Não                Sim        Não     Sim       Sim
Gestão de iFrames                  Não                Sim        Não     Sim       Não
Acessar cabeçalhos de solicitação  Sim                Não        Sim     Não       Não
Cabeçalhos de resposta             Sim                Não        Sim     Não       Não
Manipular Cookies                  Sim                Sim        Sim     Sim       Sim
Acessar códgigo de status          Sim                Não        Sim     Não       Não
Manipular mouse                    Não                Sim        Sim     Sim       Sim
Arrastar e largar                  Não                Sim        Não     Sim       Sim
Ações de teclado                   Não                Sim        Sim     Sim       Sim
Visualizar elementos               Não                Sim        Não     Sim       Sim
Avaliar JS                         Não                Sim        Sim     Sim       Sim
Redimensionar janela               Não                Sim        Não     Não       Não
Maximizar janela                   Não                Sim        Não     Sim       Não
=================================  =================  =========  ======  ========  ====