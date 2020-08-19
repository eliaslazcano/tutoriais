
# Image

- Dependencia:

`import {Image} from 'react-native'`

- Uso:
> Importação local
> `<Image source={require('../res/img/ola.jpg')}/>`

> Importação web
> `<Image source={{uri: 'https://dominio.com/img.jpg'}}/>`

# FlatList

Gera lista de conteúdos com scroll usando estrutura de repetição.

- Dependencia:

`import {FlatList} from 'react-native'`

- Uso:

> Imagine que temos um array:
> `const nomes = [{id: 1, nome: 'Elias}, {id: 1, nome: 'Karol}, {id: 1, nome: 'Jesus}]`

A geração da lista se deve assim:

```Flatlist
<FlatList
  data={ nomes }
  keyExtractor={ item => item.id.toString() }
  renderItem={ ({item}) => {
      return (
        <Text>{item.nome}</Text>
      );
    }
  }
/>
```

# TextInput

- Dependencia:

`import {TextInput} from 'react-native'`

```TextInput
let inputReference;
let inputText;
let limparCampo = function () {
  if (inputReference) inputReference.clear();
}

<TextInput
  ref={el => inputReference = el}
  placeholder={'Deixe seu comentário'}
  onChangeText={(texto) => inputText = texto}
/>

```