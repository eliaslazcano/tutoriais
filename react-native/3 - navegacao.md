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

Instale:
`npm install @react-navigation/stack`

No componente onde está sendo utilizado o `<NavigationContainer>` insira:
`import { createStackNavigator } from '@react-navigation/stack'`

```NavigationStack
import {Login, Feed} from '~/meuscomponentes'

const navigator = createStackNavigator({
  Login: {screen: Login},
  Feed: {screen: Feed},
});
const AppContainer = createAppContainer(navigator);

export default function App() {
  return (
    <AppContainer/>
  );
}
```

Trocando de tela:
`navigation.push('Feed')`

> **navigation** é recebido entre as props do componente, isto se ele for um componente que faz parte de uma rota.

### Nova forma de pilhas

Há outra forma de fazer navegação do tipo pilha, recentemente disponibilizada, o exemplo de uso é:

```
import {Login, Feed} from '~/meuscomponentes'
const Stack = createStackNavigator();
export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen name="Home" component={Login} />
        <Stack.Screen name="Feed" component={Feed} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

E se precisar passar dados para as props do componente? Exemplo de ação:
```
<Stack.Screen name="Home">
  {props => <Login {...props} extraData={someData} />}
</Stack.Screen>
```