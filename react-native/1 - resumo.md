
# React Native

O React Native é um framework baseado no já aclamado React, desenvolvido pela equipe do Facebook, que possibilita o desenvolvimento de aplicações mobile, tanto para Android, como para iOS, utilizando apenas Javascript.
Você pode **desenvolver online** pela ferramenta [Expo](https://snack.expo.io).

## Requisitos

- [NodeJs](https://nodejs.org/pt-br/)
- [python2 e jdk8](https://chocolatey.org/) (`choco install -y python2 jdk8`)
- [Android Studio](https://developer.android.com/studio)
- [Emulador Android](https://developer.android.com/studio/run/managing-avds?hl=pt-br) e [SDK instalados](https://developer.android.com/studio/intro/update#sdk-manager) (recomendo API 28)

Para completar instale o **CLI** do React Native:
`npm install -g react-native-cli`

## Comandos

Para começar um projeto: 
`npx react-native init MeuApp`

Comandos para compilar ou testar:
- `react-native run-android` - (Re-)Instala no App no Android.
- `react-native run-ios` - (Re-)Instala o App no iOS.
- `react-native start` - Liga o servidor de hot-reload.

> Pressione **R** duas vezes para dar **reload** na aplicação.

## Componentes nativos
As tags utilizadas para desenhar a tela não são HTML, mas seguindo um conceito semelhante usamos tags que constroem um componente nativo do S.O. na tela do aparelho.

- **View** - É como o **div** do html, encapsula os filhos.
- **Text** - É como o **p** do html, exibe texto na tela.
- **Image** - É como o **img** do html, exibe uma imagem na tela.
- **TextInput** - É como o **input** do tipo text, exibe um campo para digitar.
- **FlatList** - É uma tag para gerar uma ListView nativa (conteúdos empilhados que poder fazer **scroll**), comportamento semelhante ao **v-for** do **Vue**, uma estrutura de repetição.
- **TouchableOpacity** - Serve para encapsular outra tag, tornando seu filho clicável, disponibiliza a programação de um *callback* do clique. Seu nome se deve ao fato de que ao clicar no elemento ele pisca sofrendo uma rápida variação de opacidade.

## Separando comportamento por plataforma (Sistema Operacional)

É necessário a importação de Platform:
`import { Platform } from 'react-native'`

Checagem de plataforma
```Platform.OS
let mensagem;
if (Platform.OS === 'ios') mensagem = 'Está usando iOS';
```

Obtendo retorno de acordo com a plataforma
```Platform.select
const mensagem = Platform.select({
  ios: 'Usando iOS da Apple',
  android: 'Usando Android da Google',
  default: 'Usando outra plataforma, Web por exemplo!',
});
```

Renderizando um componente de acordo com a plataforma
```Platform Component
const Component = Platform.select({
  ios: () => require('ComponentIOS'),
  android: () => require('ComponentAndroid')
})();

<Component />;
```

## React Hooks

É uma forma de criar variáveis **reativas**, ou seja, se forem utilizadas no escopo das tags, ela é atualizada constantemente na tela em caso de mudanças. Também é possível monitora-las, programando uma *function* para quando houver mudança no valor.

### Criando variáveis reativas

> Para desenvolvedores **Vue**, essa utilidade é semelhante as variáveis em **data**.

É necessário a importação do **useState**:
`import React, {useState} from  'react'`

A declaração da variável:
`const [nomes, setNomes] = useState(['Elias', 'Karol'])`
> A função **useState** recebe o valor inicial da variável.
> Ela retorna um array de 2 índices, o primeiro é a variável, o segundo é uma função **setter** que você deve usar para alterar o valor dela. Ex: **setNomes(['Jesus'])**.

### Monitorando variáveis reativas

> Para desenvolvedores **Vue**, esta técnica é semelhante ao **watch**.

Usamos **useEffect** para interceptar variáveis reativas, permitindo desenvolver um bloco de código que executará caso a função **setter** da variável seja acionado.

É necessário a importação do **useEffect**:
`import React, {useEffect} from  'react'`

A implementação:
`useEffect( () => {...}, [var1, var2, var3] )`
> O primeiro parâmetro é a função.
> O segundo parâmetro é um array de variáveis reativas que serão monitoradas.
> **Atenção:** se o segundo parâmetro for um array **vazio**, a função será executada uma vez e imediatamente.

## Styles Components (Componentes estilizados)

É possível fabricar rapidamente um componente com propriedades de estilo pré-determinadas partindo das tags nativas (View, Text e etc).

Tenha a dependencia instalada:
`npm install --save styled-components`

Faça a importação da lib **styled-components/native** onde for usa-la:
`import styled from 'styled-components/native'`

Para criar componentes rapidamente use (No exemplo é uma tag **View**):
```Styled Components
export const MeuComponente = styled.View`
  flex: 1;
  background: #8B10AE; 
`;
```

Utilizando o componente acima:
```Styled components 2
import React from 'react';
import { MeuComponente } from './styles';
export default function MeuApp() {
  return(
    <MeuComponente/>
  )
}
```

## StatusBar

O **StatusBar** é um componente presente apenas uma vez na aplicação, ele é a barra superior da aplicação onde aparece os status do Smartphone como sinal WiFi, Bateria, Relógio e etc. Ele costuma ser utilizado no topo da aplicação, no mesmo escopo onde fica seu componente master/root, cercados por um Fragment (componente semântico, sem alteração visual).

Importação:
`import { StatusBar } from  'react-native'`

Utilização:
```StatusBar
<Fragment>
  <StatusBar barStyle="light-content" backgroundColor="#8B10AE" />
  <Routes />
<Fragment/>
```

Propriedades da tag:
- **barStyle**: Define a cor dos textos e ícones.
-- "light-content": branco
-- "dark-content": preto
-- "default": de acordo com o sistema operacional
- **backgroundColor**: [*Somente Android*] Cor de fundo da barra. Passe um código de cor, exemplo "#8B10AE".

> No iOS a barra não aceita backgroundColor (cor de fundo) pois nesta plataforma ela flutua sobre a aplicação com fundo transparente. Se isto for um problema para sua aplicação, contorne isso com um **marginTop: 35** na tag pai da sua StatusBar.

## [Async Storage](https://github.com/react-native-community/async-storage)

Um sistema de armazenamento de chave-valor assíncrono, não criptografado, persistente para React Native.

Instalação:
`npm install @react-native-community/async-storage`

Importação:
`import AsyncStorage from '@react-native-community/async-storage'`

Gravando valor:
`await AsyncStorage.setItem('chave', valor)`

Obtendo valor:
`const valor = await AsyncStorage.getItem('chave')`

> Somente grava String, para salvar dados complexos como array ou objetos converta para uma JSON String.

## [Navegação](https://reactnavigation.org)

Instalação
`npm install @react-navigation/native`

Instale algumas dependencias:
`npm install react-native-reanimated react-native-gesture-handler react-native-screens react-native-safe-area-context @react-native-community/masked-view`

No componente raiz (root) da aplicação (normalmente index.js ou App.js) importe esta lib **na primeira linha** do arquivo:
`import 'react-native-gesture-handler'`

Agora envolva toda a aplicação pelo componente **NavigationContainer**:
```NavigationContainer
import 'react-native-gesture-handler';
import * as React from 'react';
import { NavigationContainer } from '@react-navigation/native';

export default function App() {
  return (
    <NavigationContainer>{/* codigo do app */}</NavigationContainer>
  );
}
```