
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
- `react-native run-android`
- `react-native run-ios`
- `react-native start`

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