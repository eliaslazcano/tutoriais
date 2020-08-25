# Flutter

Flutter é o kit de ferramentas de IU do Google para a criação de aplicativos bonitos e compilados de forma nativa para celular, web e desktop a partir de uma única base de código. Sem apresentar mudanças de interface gráfica em diferentes plataformas, isso é possível porque o Flutter é renderizado na tela usando uma engine gráfica como é feito nos jogos. Isso possibilita um alto desempenho e uma facilidade de debugar a performance em FPS.

Montar a interface de uma aplicação com Flutter é como montar um LEGO, os elementos vão se encaixando pois na UI há mais algoritmos lógicos do que programação excessiva, deixando de lado a verbosidade das aplicações nativas.

## Começando

Faça a instalação do Flutter SDK e as demais ferramentas necessárias de acordo com a [documentação](https://flutter.dev/docs/get-started/install).

Criando um projeto: 

`flutter create meuApp`

Executando o projeto: 
- Listar dispositivos disponívels: `flutter devices`
- Listar emuladores disponíveis: `flutter emulators`
- Executar: `flutter run`
- Forçar um reload: Aperte `r` no terminal

Executar projeto na Web ***(BETA)***:
- Troque para versão beta do Flutter: `flutter channel beta`
- Atualize o Flutter: `flutter upgrade`
- Ative o compilador web: `flutter config --enable-web`

Ferramenta DevTools:

- Ative a ferramenta: `flutter pub global activate devtools`
- Ligue a ferramenta: `flutter pub global run devtools`
- Com a ferramenta ligada, execute o projeto com `flutter run` (Web não é compátivel), observe o terminal, haverá uma URL para colar na primeira tela da ferramenta DevTools.

## Estrutura de diretórios

A base de código deve ficar na pasta **lib**, recomendo estrutura-la com estes diretórios:
- components
- views (ou screens)
- models
- http (onde fica as funções que consomem webservice)
- database (onde fica as funções que consomem banco de dados)
- **main.dart** (o arquivo inicial por onde a aplicação dá o arranque)

## Linguagem Dart

O Dart tenta unir as facilidades do JavaScript com os recursos avançados do Java/C#. Vamos fazer uma comparação com o JavaScript:

### Variaveis

#### Criação e atribuição de variáveis 

JavaScript
```
var name = 'JavaScript';
```

Dart
```
String name = 'dart';   // Explicitamente será tipado como string.
var otherName = 'Dart'; // Implicitamente será tipado como string.
// Ambos são aceitáveis ​​no Dart.
```

#### Valor padrão

JavaScript
```
var name; // == undefined
```

Dart
```
var name; // == null
int x;    // == null
```

#### Checando null ou zero

Javascript
```
var myNull = null;
if (!myNull) {
  console.log('null é tratado como false');
}
var zero = 0;
if (!zero) {
  console.log('0 é tratado como false');
}
```

Dart
```
var myNull = null;
if (myNull == null) {
  print('use "== null" para checar null');
}
var zero = 0;
if (zero == 0) {
  print('use "== 0" para checar zero');
}
```

#### Funções

Javascript
```
function fn() {
  return true;
}
```

Dart
```
fn() {
  return true;
}

// também pode ser:
bool fn() {
  return true;
}
```

> Arrow functions também funcionam no Dart, você pode usar a mesma escrita do JavaScript.

#### Programação Assíncrona (Promisse = Future)

Basicamente o nome foi trocado de Promisse para Future. O código pode ser escrito igual ao JavaScript, usando `.then()`, `.catchError()` e `.finally()` ou `async`/`await` (unidos ao `try`/`catch`)

## Widgets (components)

Os Widgets fazem o mesmo papel que um Component (como é conhecido no React e Vue).
Há dois tipos de Widgets:
- **Stateless**: é imutável, o que significa que suas propriedades não tem poder **reativo**, todos os valores na interface são finais.
- **Stateful** possui *state* (**estado/reatividade**), podendo mudar os valores apresentados em tela, mas a implementação de um widget com *state* requer pelo menos duas classes:
  1) uma classe StatefulWidget que cria uma instância de:
  2) uma classe State. A classe é StatefulWidget, em si, é imutável e pode ser descartada e regenerada, mas a classe State persiste durante a vida útil do widget, é nela que ficam os valores reativos.

#### StatelessWidget
```
import 'package:flutter/material.dart';

class MeuWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Text('Olá mundo');
  }
}
```

#### StatefulWidget
```
import 'package:flutter/material.dart';

class MeuWidget extends StatefulWidget {
  final MeuObjeto _imutavel = MeuObjeto();

  @override
  _MeuWidgetState createState() => _MeuWidgetState();
}

class _MeuWidgetState extends State<MeuWidget> {
  final MeuObjeto reativo = MeuObjeto();

  @override
  Widget build(BuildContext context) {
    return Text('Olá mundo, ' + reativo + widget.imutavel);
  }
}
```
