# TypeScript

O TypeScript é basicamente JavaScript mas com novas funcionalidades, superando limitações como:
- Objetos com modificador de acesso  *private*  e  *public*.
- Tipagem de  variáveis, possibilitando polimorfismo.

TypeScript é escrito em arquivos **.ts** e deve ser compilado para JavaScript.
Com **hot-reload** você desenvolve enquanto ele compila automaticamente.
Erros são detectados em **tempo de compilação**, enquanto que no JavaScript são em **tempo de execução**.

# Preparativos

> Requer NodeJs
- Se o projeto não foi iniciado, execute `npm init` para gerar o **package.json**
- Instale o compilador TypeScript com `npm install typescript --save-dev`
- Na raiz do projeto crie **tsconfig.json** e escreva:
```
{
  "compilerOptions": {
    "target": "es6",        // Versão do JavaScript a compilar.
    "outDir": "app/js",     // Diretorio de saída da compilação.
    "noEmitOnError": true,  // [Opt] Em caso de erro de compilação, não gera nenhum arquivo JS.
    "removeComments": true, // [Opt] Os comentários não serão compilados para o arquivo final JS.
    "module": "system",     // Habilita uso de 'módulos' (ES6 import & export), usando a lib System.js
    "experimentalDecorators": true //Habilita uso de Decorators Functions
},
  "include": [
    "app/ts/**/*"  //Inclui as diretórios a serem compilados, neste exemplo todos os arq. e dir. em 'app/ts/'
  ]
}
```
# Compilando

Compilar: `tsc`

Liga o compilador em hot-reload: `tsc -w`

> Recomendo configurar um comando **npm run** para rodar o compilador. Adicione no objeto *scripts* os atributos: **"compile": "tsc"** e **"dev":  "tsc -w"** para rodar o compilador com **npm run compile** e **npm run dev**.

# Classes e Objetos

Como todos os comandos em JavaScript (ES6) existem no TypeScript, a orientação a objetos é semelhante, apenas acrescido de Herança, Classe Abstrata, Modificador de Acesso, Tipagens e Interface.

## Declarando uma classe:

Simples
`class MinhaClasse {...}`
> Não difere do JavaScript.

Herança
`class MinhaClasse extends OutraClasse {...}`
> Herda atributos e métodos da outra classe.

Classe Abstrata
`abstract class MinhaClasse {...}`
> Impede que a classe seja instanciada em objeto.

Implementando Interface
`class MinhaClasse implements MinhaInterface {...}`
> Interfaces definem o que uma classe deve fazer.

## Declaração de atributos

O esquema é: `[public/private/protected] varNome[: tipo]`
```
public    valor: number;
private   nome:  string;
protected data: Date;
protected carro: Automovel;
protected negociacao: Negociacao = new Negociacao();  //Declara e inicializa
protected professores: Professor[];  //array forma 1 de fazer
protected alunos: Array<Aluno>;      //array forma 2 de fazer
```

- Se o **modificador de acesso** for implícito, por padrão será **public**.
- Se o **tipo** for implícito, por padrão será **any**.
> Você pode desativar o uso do tipo **any** em **tsconfig.json** inserindo **"noImplicitAny": true** dentro de **compilerOptions**.

## Construtor
```
constructor (data: Date, quantidade: number, valor: number) {
  this.data  = data;
  this.quantidade = quantidade;
  this.valor = valor;
}
```
Você pode escrever os modificadores de acesso **public**/**private**/**protected** nos parametros do construtor, antecedendo o nome. Isso faz com que auto-gere estes dados como atributos na classe.

`constructor (private data: Date, private quantidade: number, private valor: number) {...}`

## Métodos

O esquema é `minhaFuncao(meuParam[: Tipo]) [: TipoRetorno||void] {...}`
```
adicionaAluno(aluno: Aluno, inscrito?: boolean) {
  this.alunos.push(aluno);
}
meuMetodo(): void {
  console.log('ola mundo');
}
mensagem(): string {
  return 'ola mundo';
}
professoresArray(): Professor[] {
  return [].concat(this.alunosArray);
}
```
> **Parâmetro Opcional:** use **?** no final do nome, assume **undefined** quando não utilizado.

## Getters
Os getters já existem no JavaScript e permanecem a mesma coisa.
```
get quantidade() {
  return this.quantidade;
}
get valor() {
  return this.valor;
}
get volume() {
  return this.quantidade * this.valor;
}
```

# Classe com tipo desconhecido
Lógica popular em C# e Java, muito aplicado em herança.
Você desenvolve o código usando tipagens desconhecidas, porem apelidadas.

Como criar a classe:
```
class GenericDao<TipoA, TipoB> {
  adiciona(objeto:  TipoB): TipoA  {...}
  apaga(objeto: TipoB): void  {...}
  buscaPorId(id: TipoA): TipoB  {...}
  atualiza(objeto: TipoB): void  {...}
  listaTodos(): TipoB[] {...}
}
```
> Você pode dar o nome que quiser para a tipagem recebida

Como usar a classe:
- Em herança:
`class NegociacoesView extends GenericDao<number, Aluno>{...}`
- Em objeto:
`new GenericDAO<number, Aluno>();`
