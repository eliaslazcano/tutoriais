---


---

<h1 id="flutter">Flutter</h1>
<p>Flutter é o kit de ferramentas de IU do Google para a criação de aplicativos bonitos e compilados de forma nativa para celular, web e desktop a partir de uma única base de código. Sem apresentar mudanças de interface gráfica em diferentes plataformas, isso é possível porque o Flutter é renderizado na tela usando uma engine gráfica como é feito nos jogos. Isso possibilita um alto desempenho e uma facilidade de debugar a performance em FPS.</p>
<p>Montar a interface de uma aplicação com Flutter é como montar um LEGO, os elementos vão se encaixando pois na UI há mais algoritmos lógicos do que programação excessiva, deixando de lado a verbosidade das aplicações nativas.</p>
<h2 id="começando">Começando</h2>
<p>Faça a instalação do Flutter SDK e as demais ferramentas necessárias de acordo com a <a href="https://flutter.dev/docs/get-started/install">documentação</a>.</p>
<p>Criando um projeto:</p>
<p><code>flutter create meuApp</code></p>
<p>Executando o projeto:</p>
<ul>
<li>Listar dispositivos disponívels: <code>flutter devices</code></li>
<li>Listar emuladores disponíveis: <code>flutter emulators</code></li>
<li>Executar: <code>flutter run</code></li>
<li>Forçar um reload: Aperte <code>r</code> no terminal</li>
</ul>
<p>Executar projeto na Web ***(BETA)***:</p>
<ul>
<li>Troque para versão beta do Flutter: <code>flutter channel beta</code></li>
<li>Atualize o Flutter: <code>flutter upgrade</code></li>
<li>Ative o compilador web: <code>flutter config --enable-web</code></li>
</ul>
<p>Ferramenta DevTools:</p>
<ul>
<li>Ative a ferramenta: <code>flutter pub global activate devtools</code></li>
<li>Ligue a ferramenta: <code>flutter pub global run devtools</code></li>
<li>Com a ferramenta ligada, execute o projeto com <code>flutter run</code> (Web não é compátivel), observe o terminal, haverá uma URL para colar na primeira tela da ferramenta DevTools.</li>
</ul>
<h2 id="estrutura-de-diretórios">Estrutura de diretórios</h2>
<p>A base de código deve ficar na pasta <strong>lib</strong>, recomendo estrutura-la com estes diretórios:</p>
<ul>
<li>components</li>
<li>views (ou screens)</li>
<li>models</li>
<li>http (onde fica as funções que consomem webservice)</li>
<li>database (onde fica as funções que consomem banco de dados)</li>
<li><strong>main.dart</strong> (o arquivo inicial por onde a aplicação dá o arranque)</li>
</ul>
<h2 id="linguagem-dart">Linguagem Dart</h2>
<p>O Dart tenta unir as facilidades do JavaScript com os recursos avançados do Java/C#. Vamos fazer uma comparação com o JavaScript:</p>
<h3 id="variaveis">Variaveis</h3>
<h4 id="criação-e-atribuição-de-variáveis">Criação e atribuição de variáveis</h4>
<p>JavaScript</p>
<pre><code>var name = 'JavaScript';
</code></pre>
<p>Dart</p>
<pre><code>String name = 'dart';   // Explicitamente será tipado como string.
var otherName = 'Dart'; // Implicitamente será tipado como string.
// Ambos são aceitáveis ​​no Dart.
</code></pre>
<h4 id="valor-padrão">Valor padrão</h4>
<p>JavaScript</p>
<pre><code>var name; // == undefined
</code></pre>
<p>Dart</p>
<pre><code>var name; // == null
int x;    // == null
</code></pre>
<h4 id="checando-null-ou-zero">Checando null ou zero</h4>
<p>Javascript</p>
<pre><code>var myNull = null;
if (!myNull) {
  console.log('null é tratado como false');
}
var zero = 0;
if (!zero) {
  console.log('0 é tratado como false');
}
</code></pre>
<p>Dart</p>
<pre><code>var myNull = null;
if (myNull == null) {
  print('use "== null" para checar null');
}
var zero = 0;
if (zero == 0) {
  print('use "== 0" para checar zero');
}
</code></pre>
<h4 id="funções">Funções</h4>
<p>Javascript</p>
<pre><code>function fn() {
  return true;
}
</code></pre>
<p>Dart</p>
<pre><code>fn() {
  return true;
}

// também pode ser:
bool fn() {
  return true;
}
</code></pre>
<blockquote>
<p>Arrow functions também funcionam no Dart, você pode usar a mesma escrita do JavaScript.</p>
</blockquote>
<h4 id="programação-assíncrona-promisse--future">Programação Assíncrona (Promisse = Future)</h4>
<p>Basicamente o nome foi trocado de Promisse para Future. O código pode ser escrito igual ao JavaScript, usando <code>.then()</code>, <code>.catchError()</code> e <code>.finally()</code> ou <code>async</code>/<code>await</code> (unidos ao <code>try</code>/<code>catch</code>)</p>
<h2 id="widgets-componentes">Widgets (<s>componentes</s>)</h2>
<p>Os Widgets fazem o mesmo papel que um <s>Componente</s> (como é conhecido no React e Vue).<br>
Há dois tipos de Widgets:</p>
<ul>
<li><strong>Stateless</strong>: é imutável, o que significa que suas propriedades não tem poder <strong>reativo</strong>, todos os valores na interface são finais.</li>
<li><strong>Stateful</strong> possui <em>state</em> (<strong>estado/reatividade</strong>), podendo mudar os valores apresentados em tela, mas a implementação de um widget com <em>state</em> requer pelo menos duas classes:
<ol>
<li>uma classe StatefulWidget que cria uma instância de:</li>
<li>uma classe State. A classe é StatefulWidget, em si, é imutável e pode ser descartada e regenerada, mas a classe State persiste durante a vida útil do widget, é nela que ficam os valores reativos.</li>
</ol>
</li>
</ul>
<h4 id="statelesswidget">StatelessWidget</h4>
<pre><code>import 'package:flutter/material.dart';

class MeuWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Text('Olá mundo');
  }
}
</code></pre>
<h4 id="statefulwidget">StatefulWidget</h4>
<pre><code>import 'package:flutter/material.dart';

class MeuWidget extends StatefulWidget {
  final MeuObjeto _imutavel = MeuObjeto();

  @override
  _MeuWidgetState createState() =&gt; _MeuWidgetState();
}

class _MeuWidgetState extends State&lt;MeuWidget&gt; {
  final MeuObjeto reativo = MeuObjeto();

  @override
  Widget build(BuildContext context) {
    return Text('Olá mundo, ' + reativo + widget.imutavel);
  }
}
</code></pre>
<h2 id="widgets-componentes-prontos-do-material-design">Widgets (<s>Componentes</s>) prontos do Material Design</h2>
<h4 id="introdução">Introdução</h4>
<p>Para construir rapidamente uma interface, o Flutter ja vem com duas bibliotecas de Widgets prontos para uso, Cuppertino e Material, para uma aparencia do iOS e Android respectivamente.</p>
<h4 id="scaffold---o-widget-de-partida">Scaffold - O Widget de partida</h4>
<p>O Scaffold é um Widget inicial para uma tela, ele fornece a barra do cabeçalho, um título e o body que é onde ficará o restante da tela.</p>
<h2 id="navegação">Navegação</h2>
<blockquote>
<p><strong>Terminologia:</strong> Em Flutter, rotas e telas são a mesma coisa.</p>
</blockquote>
<p>A maioria dos Widgets fazem este import:</p>
<p><code>import 'package:flutter/material.dart';</code></p>
<p>Através dele você tem acesso a classe Navigator, que possui métodos estáticos (usáveis sem instanciar objeto) mencionados a seguir.</p>
<h4 id="navegar-para-outra-tela">Navegar para outra tela</h4>
<p>Use <code>Navigator.push()</code>. O <strong>push</strong> adiciona a tela na pilha de rotas, um empilhamento gerenciado pelo <strong>Navigator</strong>.</p>
<pre><code>Navigator.push(
  context,
  MaterialPageRoute(builder: (context) =&gt; minhaTelaWidget()),
);
</code></pre>
<h4 id="retornando-para-a-tela-anterior">Retornando para a tela anterior</h4>
<p>Para voltar a tela anterior da pilha, use <code>Navigator.pop(context)</code></p>
<blockquote>
<p>O sistema de <strong>pilhas</strong> é quando uma tela vai ficando sobre a outra, por isso o termo empilhado.</p>
</blockquote>
<h3 id="navegação-com-rota-nomeada">Navegação com rota nomeada</h3>
<p>Rotas nomeadas é semelhante as URLs da Web.</p>
<h4 id="defina-as-rotas">Defina as rotas</h4>
<pre><code>MaterialApp(
  // Inicie o app com a rota de nome "/".
  initialRoute: '/',
  routes: {
    '/': (context) =&gt; PrimeiraTela(),
    '/outrarota': (context) =&gt; OutraTela(),
  },
);
</code></pre>
<h4 id="navegue-para-um-nome">Navegue para um nome</h4>
<pre><code>Navigator.pushNamed(context, '/outrarota');
</code></pre>
<blockquote>
<p>Ainda pode voltar 1 tela com <code>Navigator.pop(context)</code></p>
</blockquote>

