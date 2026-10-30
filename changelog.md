# Changelog — Help Vida

## 2026-10-30

- 2026-10-30 · Consultor · Vínculo do sistema: criado submódulo Git real `07-sistemas/Prescri-o-SES` (gitlink `160000`, commit `41df705`) apontando para o repositório do cliente `FernandoHelpVida/Prescri-o-SES`. `.gitmodules` publicado com URL limpa (sem credencial); registro em `07-sistemas/Prescri-o-SES-vinculo.md`. Nenhuma fase, task, SPEC ou aceite alterado.
- 2026-10-30 · Fernando/TI · Task F1-T01 concluída: teste humano aprovado pelo champion ("está tudo de acordo"); revalidação independente confirmou migrações 0001/0002 aplicadas, regras de acesso e hooks de RBAC/auditoria intactos e prévia renderizando login (v0.0.7). Evidências: painel admin + logs do projeto Skip "Novo Projeto" (56877).
- 2026-10-30 · Fernando/TI · Paleta da marca Help Vida aplicada ao tema (v0.0.8): tokens em `src/main.css` e `tailwind.config.ts` reancorados na logo oficial (verde escuro #06301F, teal #128A68, verde claro #6FC7AE, amarelo #D3B308, fundo #F4F6F5); QA passou em setup, análise estática, build e integrações; prévia confere as cores na tela de login. Sem alteração de regra, dado ou hook.
- 2026-10-30 · Fernando/TI · Emenda E-1 proposta na SPEC-1-002: contrato `B-ARQ-01` passa a modelar lote de N páginas por ocorrência (mínimo proposto de 20), com página indexada, hash e qualidade próprios. **Aguardando homologação de Fernando/TI** — nenhum valor implementado.

## 2026-09-15

- 2026-09-15 · Fernando/TI · F1-T01: implementação restrita concluída no projeto Skip "Novo Projeto" (versão 0.0.5); migrações `0001_hv_access_control` e `0002_hv_harden_user_access` aplicadas; QA oficial passou em setup, análise estática, build, integrações e teste; teste humano ainda pendente.
- 2026-09-15 · Fernando/TI · DEBUG task F1-T01: app ficou em branco na prévia v0.0.4 → causa raiz `ReferenceError` na montagem de `Index.tsx` (bloco de provas inserido em `Login`, fora do escopo de `user`, `proofOccurrence` e `runProof`) → corrigido na v0.0.5.

## 2026-09-08

- Workspace externo da Fase 1 preparado a partir do handoff validado.
- Incluídas cinco SPECs e F1-T01..F1-T10.
- Ata de corte de 03/09 incluída sem transcrição bruta.
- Nenhuma implementação, integração, conta, repositório ou conector criado.