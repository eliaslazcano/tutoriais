# [Navegação](https://reactnavigation.org)

## Preparativos

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

## Tipos de navegação

### Pilha

Este tipo de navegação **empilha** uma tela sobre a outra, significa então que você poderá retornar para a tela anterior na mesma sequencia. Automaticamente este método gera uma barra no topo da aplicação com o título da tela e uma seta de voltar, podendo ser personalizada ou até removida.

Instale:
`npm install @react-navigation/stack`

Criando uma navegação **pilha**:
```NavigationStack
// Em App.js no seu novo projeto

import * as React from 'react';
import { View, Text, Button } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';

function TelaInicial(props) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>Tela Inicial</Text>
      <Button title="Trocar de tela" onPress={() => props.navigation.navigate('Detalhes')}/>
    </View>
  );
}

function TelaAdicional(props) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>Tela Adicional</Text>
      <Button title="Abrir 'Detalhes' de novo" onPress={() => props.navigation.push('Detalhes')}/>
      <Button title="Voltar" onPress={() => props.navigation.goBack()} />
    </View>
  );
}

const Stack = createStackNavigator();

function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen name="Home" component={TelaInicial} />
        <Stack.Screen name="Detalhes" component={TelaAdicional} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

export default App;
```

> **A propriedade **navigation****:
> Os componentes Screen sempre recebem a prop **navigation**.
>> `navigation.navigate('NomeDaRota')` navegará para a tela desejada, a menos que ja esteja nela. Se usar `navigate` em uma tela que já está na pilha, você voltará para ela.
>
>> `navigation.push('NomeDaRota')` navegará para a tela desejada, mesmo que ja esteja nela, forçando empilhar outra por cima.
>
>> `navigation.goBack()` voltará para a tela anterior da pilha.

#### Passando dados para a próxima tela:

O segundo parametro de **navigate** e **push** é um objeto que transportará os dados.

`navigation.navigate('NomeRota', {autor: 'Elias', idade: 25})`

O componente a seguir receberá os dados na prop `route`:
```Passando dados
function MeuComponente(props) {
  const { autor } = route.params;
  const { idade } = route.params;
}
```

Se você não especificou nenhum parâmetro ao navegar para esta tela, os parâmetros iniciais serão usados. Para definir parametros iniciais faça assim no componente Screen:
```
<Stack.Screen
  name="MinhaRota"
  component={MeuComponente}
  initialParams={{ idade: 25 }}
/>
```

> As telas também podem atualizar os params recebidos, aproveitando o poder de reatividade na interface.
> Basta utilizar o `navigation.setParams`.

#### Passando dados para a tela anterior:

Para fazer isso, você pode usar o método `navigate`, que funciona como `goBack` se a tela já existe. Usando o segundo parametro para enviar dados como ensinado anteriormente. Quando navegar para a outra tela `route.params` será atualizada para refletir os dados você enviou.