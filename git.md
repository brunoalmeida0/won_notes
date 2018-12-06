# Git e GitHub

## Configurações básicas

### Ver as configurações do Git

Use o atributo --list para ver todas as configurações ou o nome do atributo que desejar visualizar.

```bash
git config --list
```

### Configurando nome de user 

```bash
git config --global user.name "seu nome"
```

### Configurando e-mail de user

```bash
git config --global user.email "seu@email.gg"
```

### Configurando editor principal

Atalho do editor sem aspas.

```bash
git config --global core.editor "atalho do editor"
```

## Repositórios

Para iniciar um repositório do Git é só acessar a pasta do projeto que deseja transformar em repositório e executar o comando:

```bash
git init
```

### Ciclo de vida dos status dos arquivos

- Untracked
- Unmodified
- Modified
- Staged

### Status atual do repositório

```bash
git status
```

