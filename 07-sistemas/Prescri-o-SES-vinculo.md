# Prescri-o-SES — vínculo com o repositório operacional

**Status: submódulo Git REAL (gitlink confirmado).**

Esta pasta registra o vínculo entre a raiz operacional da Help Vida e o repositório de código do sistema construído no Skip. Diferente de um registro apenas documental, o vínculo aqui é um **submódulo git de verdade**.

## 1. Identificação

| Item | Valor |
|---|---|
| Caminho do submódulo | `07-sistemas/Prescri-o-SES` |
| Repositório do código | https://github.com/FernandoHelpVida/Prescri-o-SES.git |
| Raiz operacional | https://github.com/ramonpadua/Helpvida-adapta-Cliente |
| Commit fixado do sistema | `41df705` |
| Modo git esperado | `160000` (gitlink) |
| Data do vínculo | 2026-10-30 |

**Titularidade:** o repositório de código é do **cliente** (organização GitHub `FernandoHelpVida`), conforme a divisão de trabalho do projeto: conta, repositório e credenciais são do cliente; o consultor mantém o repositório operacional e o vínculo.

## 2. O que foi feito

1. Criado `.gitmodules` com o caminho `07-sistemas/Prescri-o-SES` e a URL pública do repositório.
2. Criado o gitlink (modo `160000`) apontando para o commit `41df705` do repositório do cliente.
3. Verificado no GitHub que a entrada aparece como submódulo (tipo `commit`).

**Nenhuma credencial foi gravada** no `.gitmodules`: a URL publicada é a limpa, sem token. O token de acesso usado para clonar ficou apenas na configuração local do ambiente, fora do versionamento.

## 3. Como consumir

```bash
git clone https://github.com/ramonpadua/Helpvida-adapta-Cliente.git
cd Helpvida-adapta-Cliente
git submodule update --init --recursive
```

A leitura do código exige acesso ao repositório privado `FernandoHelpVida/Prescri-o-SES` (é `private`). Quem não tiver permissão clona a raiz, mas o submódulo fica vazio.

## 4. Divisão de responsabilidade

- **Código do sistema:** evoluído pelo cliente no Skip, que espelha no repositório dele a cada sync (commits automáticos do tipo "Auto-commit before sync" + versões `v0.0.x`).
- **Raiz operacional:** mantida pelo consultor — fases, SPECs, tasks, STATUS e changelog.
- **O vínculo não sincroniza automaticamente:** atualizar o ponteiro é um commit deliberado na raiz (`git submodule update --remote` + commit), não acontece sozinho.

## 5. O que este vínculo NÃO faz

- Não clona, builda nem publica o sistema.
- Não altera fases, tasks ou aceites do projeto.
- Não garante que o código em produção esteja igual ao commit fixado — a conferência de estado do app é feita pelo Skip, não por este repositório.

## 6. Observação de rastreabilidade

Como o Skip faz commits automáticos frequentes, o commit fixado aqui (`41df705`) é um **retrato** do sistema nesta data, não a versão viva. Ao conferir divergências entre o que o cliente relata e o que está publicado, comparar com o histórico do repositório do cliente antes de assumir que houve avanço.
