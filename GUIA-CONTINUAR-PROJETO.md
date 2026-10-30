# Guia de retomada — Help Vida / SES

## Ao Fernando dizer “vamos continuar o projeto”
1. Ler AGENTS.md, STATUS.md, este guia, fase.md e SPEC-1-006. Conferir branch/código atual antes de escrever; preservar T01 e todas as alterações já aceitas. Repositório operacional e sistema não são o mesmo repo: código está no submódulo `07-sistemas/Prescri-o-SES`.
2. Responder em linguagem simples: **“A tela de envio, os cadastros e o agente já estão no código. O próximo passo é corrigir a ligação da leitura: hoje o sistema passa só o nome do arquivo e, se a leitura falha, preenche exemplos. Vamos retirar esses resultados inventados e deixar o teste seguro, sem refazer sua tela.”**
3. Dizer o que será mexido: hook `pocketbase/hooks/hv_extrair_prontuario.js`, tratamento de erro dos cards/serviço da tela e testes correspondentes da T11. Não iniciar lote, SharePoint/API ou task seguinte junto.
4. Apresentar o plano curto da T11 e pedir uma única autorização se ainda não existir: “Posso fazer essa correção agora?”. Se Fernando disser “pode continuar/corrigir” após a explicação, registrar o trecho como autorização desta task e executar; não ficar repetindo a pergunta. “Vamos continuar” sozinho inicia orientação/análise, não autoriza implementar tudo.

## Conferir o agente sem criar duplicado
- No código 41df705, migration `0005_leitor_prontuarios_helpvida.js` declara `leitor-prontuarios-helpvida`; `prontuario-extractor` é compatibilidade. O hook já chama o agente. **Declarado em código não prova instalado no ambiente.**
- O Maestro do cliente, conectado ao Skip correto (projeto 56877, organização da Soraya), deve consultar agentes/migrations/logs e confirmar que 0005 foi aplicada e o slug existe; descrever configuração sem segredos. Reutilizar agente existente. Se não houver acesso, explicar a pendência e orientar o Fernando, sem afirmar confirmação remota.
- Neste assistente externo, consulta direta retornou `Project not found`; portanto não foi confirmada instalação em execução.
- O problema não se resolve apenas anexando filename/URL ou trocando fast por reasoning. Para ler foto é preciso um caminho documentado que processe o conteúdo visual/OCR. Se indisponível, T11 entrega falha explícita + modo manual, sem inventar resultado. Leitura visual real é prova T06, não promessa de T11. Serviço externo só após decisão/gates; não pedir chave por chat.

## Primeiro teste humano — explicar assim, depois das provas técnicas
O agente deverá fornecer o LINK REAL da prévia que acabou de verificar, papel/conta de teste adequada e caminho exato. Referência registrada: https://novo-projeto-f88ac--preview.goskip.app (conferir atual antes de orientar). Nunca mandar senha no chat nem usar dados reais.

**Passo a passo para o Fernando:**
1. Abra o link da prévia indicado na resposta e faça login com sua conta de teste. Não precisa abrir banco de dados nem procurar hook.
2. No menu, clique em **“Anexar prontuário”**. Selecione um paciente fictício em **“Cliente”** antes de anexar.
3. Para o primeiro teste, use **“Prontuário nítido demo”** ou **“Enviar arquivo”** com a imagem sintética fornecida pelo agente. Não use prontuário real. Nesta task é um arquivo; lote será completado depois.
4. Clique em **“Enviar para conferência”**. Confira protocolo, prévia da imagem e os campos ao lado.
5. Se a leitura não estiver disponível, deve aparecer aviso claro de modo manual, com campos vazios/desconhecidos. **Não pode aparecer data/profissional/nome inventados nem confiança alta sem leitura.** Não deve perder a imagem nem o protocolo.
6. Use **“Teste imagem ilegível”**. Deve pedir conferência manual/avisar indisponibilidade; nenhuma identidade/data deve ser deduzida do filename ou cadastro.
7. Para revisar, entre como conferente de teste (ou admin com permissão), abra a fila de conferência e localize o protocolo. O agente deve validar esse caminho e dizer o nome de tela/botão atual; se a fila ainda não permitir revisão manual completa, explicar o que está disponível agora e registrar a lacuna na tarefa correspondente, sem chamar o teste de aprovado.
8. Onde a tela permitir, confira a foto e os três campos previstos e use **“Confirmar dados”**. Operador não aprova. Confirmação em estado inválido é falha, não “funcionou”.
9. Volte ao Maestro e diga **“Testei e funcionou: não inventou dados, mostrou o aviso e preservou a imagem”** ou relate passo, protocolo sintético e erro. O agente pede captura sanitizada apenas se precisar; não pede credenciais/imagem real.

O agente primeiro roda testes técnicos controlados de erro/JSON inválido/sem conteúdo visual. Botão demo ajuda visualização, mas não prova capacidade de leitura. O teste de imagem nítida não deve se tornar falso sucesso só porque a fixture é conhecida.

## Depois do teste
Registrar evidência + aceite expresso só da T11. Se falhar, corrigir a mesma task. Se aprovado, explicar T02 em linguagem simples e solicitar autorização separada antes de implementar. Não marcar T03/T05/T06 como concluídas por este teste nem alterar T01.

## Fluxo SES recebido em 30/10 — fonte incorporada

Fonte: `FLUXO_ADAPTA_SES.docx`, Drive ID `1gJyymfrmYRe16tcogQfdjK4JCWvWse5_` (contexto), lido integralmente. **A entrega do fluxo pelas meninas está cumprida: não voltar a cobrá-lo.**
O documento confirma faturamento por pacote, auditoria de prescrições/evoluções manuscritas, carimbo/assinatura/legibilidade/rasuras, relatórios mensais por terapia e confronto com o **SpinCare**. Corrige a transcrição “Skin Care”: nome do sistema confirmado documentalmente como SpinCare; documentação/endpoints/autenticação da API ainda não foram entregues/provados.
Categorias incluem medicina, enfermagem, fisioterapia, fonoterapia, nutrição, serviço social, psicologia e relatórios de técnicos. Presença/legibilidade são conferidas sem atribuir identidade por rubrica.
Referência de pacote: baixa 6h técnico/fisio 3 por semana/fono 1; média 12h/3/1; alta sem ventilação 24h/5/2; alta com ventilação 24h/7/2. Visitas médica e enfermagem semanais; nutrição, serviço social e psicologia mensais. **Prevalece sempre autorização individual/vigência**, não aplicar frequência global nem automatizar cobrança/diagnóstico. Regras e confronto gerencial para etapa própria, não extrair narrativa clínica nesta correção.
O fluxo descreve processo institucional atual; fotos semanais antecipam preparação, não substituem automaticamente prontuário físico/relatórios assinados nem liberam faturamento. T07 já tem insumo de fluxo; formato de saída versionado e aceite operacional ainda precisam ser homologados, sem pedir ao cliente que entregue o mesmo fluxo novamente.
