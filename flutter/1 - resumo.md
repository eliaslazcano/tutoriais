# Flutter

Flutter é o kit de ferramentas de IU do Google para a criação de aplicativos bonitos e compilados de forma nativa para celular, web e desktop a partir de uma única base de código.

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

## Widgets (components)

Os Widgets fazem o mesmo papel que um Component (como é conhecido no React e Vue).

StatelessWidget
```
import 'package:flutter/material.dart';

class MeuWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Text('Olá mundo');
  }
}
```

StatefulWidget
```
import 'package:flutter/material.dart';

class MeuWidget extends StatefulWidget {
  @override
  _MeuWidgetState createState() => _MeuWidgetState();
}

class _MeuWidgetState extends State<MeuWidget> {
  @override
  Widget build(BuildContext context) {
    return Text('Olá mundo');
  }
}
```