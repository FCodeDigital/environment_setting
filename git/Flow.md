
## Como funciona?

O Git Flow trabalha com duas branches principais, a Develop e a Master, que duram para sempre; e três branches de suporte, Feature, Release e Hotfix, que são temporários e duram até realizar o merge com as branches principais.

Então, ao invés de uma única branch Master, esse fluxo de trabalho utiliza duas branches principais para registrar o histórico do projeto. A branch Master armazena o histórico do lançamento oficial, e a branch Develop serve como uma ramificação de integração para recursos.

É ideal que todos os commits na branch Master sejam marcados com um número de versão.

### Branch Master

Principal branch, aqui é onde temos todo o código de produção. Todas as novas funcionalidades que estão sendo desenvolvidas, em algum momento, serão mescladas ou associadas a Master. As formas de interagir com essa branch são através de uma Hotfix ou de uma nova Release.

### Branch Develop

É a branch onde fica o código do próximo deploy. Ela serve como uma linha do tempo com os últimos desenvolvimentos, isso significa que ela possui funcionalidades que ainda não foram publicadas e que posteriormente vão ser associadas com a branch Master.

### Branch Feature

São branches utilizadas para o desenvolvimento de funcionalidades específicas. É recomendável que essas branches sigam uma convenção de nome, a convenção mais utilizada é iniciar o nome das branches com feature, por exemplo, `feature/fcode-test`.

É importante saber que essas features branches são criadas sempre a partir da branch Develop. Portanto, quando finalizada, elas são removidas após realizar o merge com a Branch Develop. Se tivermos dez funcionalidades a serem desenvolvidas, criaremos dez branches independentes.

É importante salientar que as branches de features não podem ter interação com a branch master, apenas com a branch develop.

### Branch Hotfix

É uma branch criada a partir da master para realizar correções imediatas encontradas no sistema em produção. Quando concluída, ela é excluída após realizar o merge com as branches Master e Develop.

Temos uma branch de hotfix para cada hotfix que precisamos implementar!

A grande diferença entre Feature Branches e Branches de Hotfix é que os Hotfix são criados a partir da Branch Master e quando os finalizamos, eles são mesclados tanto na Branch Master quanto na branch de desenvolvimento. Isso ocorre porque o bug está em ambos os ambientes.

Além disso, quando fechamos um Hotfix Branch, temos que criar uma tag com a nova versão do projeto. Isso porque cada mudança que fazemos na Branch Master precisa de uma tag que a represente.

### Branch Release

Uma vez que uma etapa de desenvolvimento esteja concluída, teremos em nossa Branch Develop todas as features e Hotfix mesclados. Então, se quisermos ter todas essas novas funcionalidades na Branch Master, teremos que criar uma Branch de Release.

A Branch Release serve como ponte para fazer o merge da Develop para a Master. Ela funciona como ambiente de homologação e é removida após realizar os testes do merge com a Master. Caso seja encontrado algum bug e haja alguma alteração, ela também deve ser sincronizada com a Develop.

Por fim, quando fechamos uma Branch Release, temos que criar uma tag com a nova versão de lançamento do software, para que possamos ter um histórico completo do desenvolvimento.


## Implementação do Git Flow

Existem duas formas de implementar o Git Flow, a primeira é utilizar os comandos básicos do Git, a outra é utilizar uma CLI que ajuda a simplificar o fluxo do Git Flow. A título de curiosidade, veremos como implementar o Git Flow utilizando as duas formas.

Para instalar a CLI do Git Flow, escolha uma opção de acordo com seu sistema operacional:

OSX: `brew install git-flow`
Linux: `apt install git-flow`
Windows: [https://git-scm.com/download/win](https://git-scm.com/download/win) → Já está incluído no Git a partir da versão 2.5.3.

## Iniciando o Git Flow

A primeira coisa que temos que fazer é criar uma Branch Develop a partir da Branch Master. Para isso, utilize:

```bash
git flow init
```

ou com a CLI básica do Git:

```bash
git checkout -b develop
```

## Branch Feature

### Criação de uma feature

Com comandos básicos do Git:

```bash
git checkout develop
git checkout -b name-feature
```

Com a CLI do Git-flow:

```bash
git flow feature start name-feature
```

### Finalização de uma feature

Com comandos básicos do Git:

```bash
git checkout develop
git merge name-feature
```
Com a CLI do Git-flow:

```bash
git flow feature finish name-feature
```

## Branch Hotfix

### Criação de um Hotfix

Com comandos básicos do Git:

```bash
git checkout master
git checkout -b name-hotfix
```

Com a CLI do Git-flow:

```bash
git flow hotfix start name-hotfix
```

### Finalização de um Hotfix

Com comandos básicos do Git:

```bash
git checkout master
git merge name-hotfix
git checkout develop
git merge name-hotfix
git tag name-hotfix
```

Com a CLI do Git-flow:

```bash
git flow hotfix finish name-hotfix
```

Aqui podemos ver o quão útil é a CLI do Git-flow, pois simplifica o processo e nos ajuda a não cometer erros.

## Branch Release

### Criação de uma Release

Com comandos básicos do Git:

```bash
git checkout develop
git checkout -b release/1.0.0
```

Com a CLI do Git-flow:

```bash
git flow release start 1.0.0
```

### Finalização de uma Release

Com comandos básicos do Git:

```bash
git checkout master
git merge release/1.0.0
git checkout develop
git merge release/1.0.0
git tag 1.0.0
```

Com a CLI do Git-flow:

```bash
git flow release finish 1.0.0
```

Pronto, agora sabemos como utilizar os comandos do Git e a CLI git-flow para aplicarmos o Git Flow na prática!