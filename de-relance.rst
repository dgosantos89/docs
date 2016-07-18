Mink de Relance
===============

Há um enorme número de emuladores de navegadores lá fora, como `Goutte`_, `Selenium`_,
`Sahi`_ e outros. Todos eles fazem o mesmo trabalho, mas o fazem diferentemente.
Eles se comportam diferentemente e tem muitas API's diferentes. Mas, o que é mais 
importante, há na verdade 2 tipos completamente diferentes de emuladores de navegadores lá fora:

* Emuladores de navegadores Headless (sem interface gráfica)
* Controladores de navegador

O primeiro tipo de emuladores de navegadores são implementações pura e simples de especificação HTTP, 
como `Goutte`_. Esses emuladores de navegadores enviam uma requisição HTTP real contra uma aplicação 
e analisam o conteúdo da resposta. Eles são muito simples de executar e configurar, porque este tipo 
de emulador pode ser escrito em qualquer linguagem de programação disponível e pode ser executado 
através do console em servidores sem GUI. Emuladores Headless tem vantagens e desvantagens. 
As vantagens são simplicidade, velocidade e habilidade para o executar sem a necessidade de um 
navegador real. Mas este tipo de navegadores tem uma grande disvantagem, eles não suportam JS/AJAX. 
Então, você não pode testar suas ricas aplicações web GUI com navegadores headless.

O segundo tipo de controladores são os emuladores de navegadores. Estes emuladores visam controlar 
o emulador real. É isto mesmo, um programa para controlar outro programa. Controladores de Navegadores 
simulam as interações dos usuários no navegador e são capazes de recuperar a informação atual da atual 
página de navegador. `Selenium`_ and `Sahi`_ são os dois controladores de navegadores mais famosos. 
A principal vantagem do uso de controladores de navegadores é o suporte a interações JS/AJAX na página. 
A disvantagem que tal emuladores de navegadores exigem a instalação do navegador, configurações extra e 
geralmente são mais lentos do que headless em contrapartida.

Então, a resposta fácil é escolher o melhor emulador para o seu projeto e usar a sua API para testes. 
Mas como nós já vimos, ambos tipos de emuladores de navegadores tem vantagens e desvantagens. Se você 
escolher o headless, você não será capaz de testar suas páginas JS/AJAX. E se você escolher o controlador 
de navegador, sua suite de testes vai se tornar muito lenta em algum ponto. Então, no mundo real nós devemos 
usar ambos! E é por isso que vocẽ precisa do **Mink**.

O **Mink** remove as diferentes API entre diferentes emuladores de navegador fornecendo diferentes drivers 
(leia no capítulo :doc:`/guides/drivers`) para todos os emuladores de navegador e provê uma forma fácil de 
controlar o navegador (:doc:`/guides/session`), atravessar páginas (:doc:`/guides/traversing-pages`), 
manipular elementos da página (:doc:`/guides/manipulating-pages`) ou interagim com eles (:doc:`/guides/interacting-with-pages`).

.. _Goutte: https://github.com/FriendsOfPHP/Goutte
.. _Sahi: http://sahi.co.in/w/
.. _Selenium: http://seleniumhq.org/
