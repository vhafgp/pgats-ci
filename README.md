[![Code coverage badge](https://img.shields.io/badge/coverage-100%25-brightgreen)](https://stryker-mutator.io/robo-coasters-example/reports/coverage/lcov-report/index.html)
[![Mutation testing badge](https://img.shields.io/endpoint?style=flat&url=https%3A%2F%2Fbadge-api.stryker-mutator.io%2Fgithub.com%2Fstryker-mutator%2Frobo-coasters-example%2Fmaster)](https://dashboard.stryker-mutator.io/reports/github.com/stryker-mutator/robo-coasters-example/master)

# PGATS - CI

## Pré-requisitos

1. Instale o [git](https://git-scm.com)
2. Instale o [nodejs](https://nodejs.org/)
3. Instale o Yarn - `npm install -g yarn`
4. Faça um _Fork_ do projeto
5. Clone o repositório para sua máquina (seu fork)
6. Instale as dependências
   ```shell
   cd pgats-ci
   yarn
   ```
7. Execute os testes de unidade - isso vai gerar um relatório
   ```shell
   yarn run test
   ```
8. Abra o relatório de cobertura de código em `reports/coverage/lcov-report`
9. Execute os testes de mutação com o Stryker
   ```shell
   yarn run test:mutation
   ```
10. Abra o relatório de mutação em `reports/mutation`
11. Instale os navegadores do Playwright
    ```shell
    yarn playwright install
    ```
12. Execute os testes end-to-end com o Playwright
    ```shell
    yarn run e2e
    ```
13. Execute a aplicação com `yarn start`
14. Acesse a aplicação publicada [neste link](https://pgats-ci-example.netlify.app)

---

💜⚡️
# pgats-ci

---

## Atividades Extra

A ferramenta usada na disciplina foi o **GitHub Actions**, então usei a pipeline criada na aula (`.github/workflows/01-manual-exec.yaml`) como base nos três exercícios.

**Exercício 1 (outra ferramenta de CI)** ([`.circleci/config.yml`](.circleci/config.yml)): repliquei a pipeline no **CircleCI**. Ele lê o repositório direto do GitHub e roda os mesmos passos da aula: instalar as dependências, instalar os navegadores do Playwright e rodar os testes e2e.

**Exercício 2 (action do Marketplace)** ([`.github/workflows/02-e2e-com-relatorio.yml`](.github/workflows/02-e2e-com-relatorio.yml)): a pipeline da aula com uma action a mais, a `actions/upload-artifact`, que publica o relatório HTML do Playwright como artefato pra download.

**Exercício 3 (self-hosted agent)** ([`.github/workflows/03-self-hosted.yml`](.github/workflows/03-self-hosted.yml)): registrei a minha própria máquina como runner self-hosted do GitHub Actions (`runs-on: self-hosted`) e rodei a pipeline nela, em vez de uma máquina da nuvem. A avaliação está logo abaixo.

### Exercício 3: avaliação

**Quando faz sentido usar um self-hosted runner/agent?**

Quando você precisa de mais controle do que a máquina da nuvem te dá. Os casos mais comuns:

- Hardware ou sistema operacional específico que a nuvem não oferece (build de iOS precisa de macOS, GPU, ARM, dispositivos físicos).
- Acesso a uma rede interna ou VPN, pra testar serviços ou bancos que só existem dentro da empresa.
- Custo: quando o volume de execução é alto, manter uma máquina própria sai mais barato que pagar minutos de nuvem.
- Cache: dá pra manter as dependências e os navegadores em cache entre as execuções e deixar o build mais rápido.

A contrapartida é que você passa a ser responsável por manter e atualizar essa máquina, e ela pode acumular estado (o famoso "na minha máquina funciona"), enquanto a máquina da nuvem começa limpa toda vez.

**Outras plataformas têm o mesmo recurso?** Têm, muda só o nome: o GitHub Actions chama de self-hosted runners, o GitLab de GitLab Runner, o CircleCI de self-hosted runners, o Jenkins de agents/nodes e o Azure DevOps de self-hosted agents.
