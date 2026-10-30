# E-F1-20261030-02 — reconciliação do desenvolvimento Help Vida

Pedido expresso de Ramon: considerar prompts enviados hoje, a call de alinhamento, o código atual e ajustar somente tarefas sequentes, preservando o já feito.

Fontes: [Call 30/10](https://drive.google.com/file/d/1N73bjPJcKf6tWYIYvEdkgnvmBDuO3dcG/view); [código 41df705](https://github.com/FernandoHelpVida/Prescri-o-SES/tree/41df70576db42daea6f9491383b235e78ae099b8); [raiz operacional](https://github.com/ramonpadua/Helpvida-adapta-Cliente).

## Cortes e limites
- Call corrige prioridade para SES (não Unimed), fotos semanais antes da coleta; paciente selecionado antes; capacidade mínima suportada de 20 fotos/lote, não máximo nem exigência de 20 em toda visita.
- Retenção para prova confirmada. SharePoint como direção; servidor local só estudo. Não existe integração de guarda provada.
- Campos nome/data/carimbo/assinatura e identificação/categoria profissional; várias evoluções; narrativa clínica não entra. Autorização varia por paciente, regras de frequência/cobrança não viram constantes da IA.
- Consulta pacientes prometida depende de documentação/prova. Sync 03h pertence ao outro projeto, não é implementação deste.
- Artefato visual já existe. Agente existe, mas hook não transmite imagem; fallback cria profissional/data/resultados fictícios. T11 é correção dentro de integridade exigida, não nova promessa de OCR.
- `npm test` é placeholder; testes humanos/funcionais não inferidos. T01 única aceita. Não apagar originais nem converter demonstração em aceite.

## Preservações
T01 da raiz, bloco completo e recibo de teste humano 11:57, permanecem intactos. UUIDs 10 tarefas legadas e revisão de fase preservados. T09/T10 suspensas, não excluídas. Code/submodule, frontend e coleções reais não modificados. Prazos antigos documentados como histórico; novo calendário a combinar, sem datas inventadas.

## Próxima ação segura
Selecionar e autorizar F1-T11; exigir prova de falha sem resultado inventado e teste humano antes da próxima. Cadastro/upload/conferência manual continuam sendo base de desenvolvimento.
