PythonToScala
=============
![PyToScala](https://farm4.staticflickr.com/3865/14938431420_58b1ffaaa9.jpg)

O objetivo desse e-book é ser um guia rápido para transição de Python para Scala. Isso de modo algum pretende ser um guia completo de Scala, mas tem "pedaços" de código para ajudar a transição entre as duas linguagens.

Esse guia segue discretamente o texto [Scala for the Impatient](http://www.horstmann.com/scala/index.html), um excelente livro introdutório para aqueles que querem aprender Scala. Você pode ler esse texto junto com outros capítulos desse e-book.

Observe que em geral, não devemos tentar traduzir diretamente expressões de uma linguagem para outra, você não quer escrever código em Scala como se escreve em Python, você quer escrever código em Scala como se escreve em Scala. por isso devemos nos esforçar para escrever código idiomático sempre que possível. Um bom ponto de início é o exemplo do Twitter [Effective Scala](http://twitter.github.io/effectivescala/)

Eu recomendo ler esse guia completamente seguindo essa ordem:

1. Variáveis e Operações Aritméticas
2. Estruturas Condicionais
3. Funções
4. Strings
5. Sequencias
6. Maps
7. Tuplas
8. Exceções
9. Classes

Aqui estão alguns tópicos em Scala não discutidos acima e que são importantes:

* **Pattern Matching** É muito poderoso e frequentemente usado, no livro [Scala Cookbook](http://shop.oreilly.com/product/0636920026914.do) existem exemplos práticos de como isso pode ser util.
* **Auxiliary Constructors** Classes podem ter vários construtores que operam em diferentes tipos e números de argumentos;
* **Case Classes** como *immutable*, *record-like* e estrutura de dados podem ser *pattern-matched*.
* **Scala Collections** Existe muito poder em todos os métodos disponíveis em estruturas de dados como Vetores, Arrays, Listas, Sequencias, Set, etc. Recomendo uma breve leitura na documentação na [documentação](http://www.scala-lang.org/api/current/index.html#scala.collection.Seq) desse métodos.

Esse conteúdo também pode ser lido no [GitBook](http://wrobstory.gitbooks.io/python-to-scala/) que oferece versões em pdf/e-book para download e no formato html.
