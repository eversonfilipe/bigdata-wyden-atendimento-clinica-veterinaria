# Projeto de BigData 2025.2

### Resumo curto
Projeto acadêmico para captura, processamento e análise de registros de atendimento veterinário, concebido para demonstração e avaliação na ExpoTech 2025.2. Objetivo principal: prover um fluxo reprodutível de dados clínicos que apoie a comunicação entre atendente e clínico e forneça sugestões analíticas de apoio à interpretação clínica.

### Status
MVP pronto para demonstração e avaliação acadêmica.

---

## Índice
- Visão e proposta de valor
- Escopo do MVP para ExpoTech 2025.2
- Entregáveis e evidências para a banca
- Equipe e responsabilidades
- Passo a passo da demonstração (runbook conceitual)
- Governança de dados, privacidade e retenção
- Critérios de avaliação e métricas operacionais
- Como contribuir e processo colaborativo
- Roadmap pós-expo
- Contatos

## Visão e proposta de valor
VetCare BigData organiza registros de atendimento clínico em um fluxo controlado e auditável. Valor central:
- Reduzir atrito entre registro e análise clínica.
- Permitir rastreabilidade e reproducibilidade das análises.
- Fornecer apoio inicial à interpretação clínica de forma responsável, com ênfase em transparência e limitações explícitas.
Essa solução é construída como um artefato acadêmico: documentada, avaliável e passível de evolução.

## Escopo do MVP para ExpoTech 2025.2
O escopo prioriza demonstrabilidade e rigor metodológico, não amplitude de produto:
- Interface de registro e consulta de atendimentos capaz de suportar um fluxo completo de uma visita.
- Pipeline reprodutível de ingestão, validação e processamento de amostras de dados para análise.
- Conjunto de amostras preparado para demonstração, com medidas de anonimização para dados pessoais.
- Módulo de suporte à interpretação clínica em versão baseline, acompanhado de documentação de avaliação e limitações.
- Material de apresentação estruturado para a banca: relatório técnico, slides e roteiro de demonstração.

## Entregáveis e evidências para a banca
O que demonstrar na banca e por quê:
- Fluxo reprodutível end-to-end para que a banca confirme a execução das etapas.
- Conjunto de amostras processadas que evidenciem qualidade e consistência dos dados.
- Relatório técnico que explique decisões, metodologia e limitações.
- Demonstração ao vivo do registro de uma visita, consulta de perfil e geração de sugestão analítica.
- Documento de privacidade e política de retenção que mostre conformidade com práticas responsáveis.

## Equipe e responsabilidades
- Éverson Filipe Campos da Silva Moura: coordenação da documentação e produto.
- Kaiky Cabral: concepção do domínio, definição de requisitos e validação clínica conceitual.
- José Emerson: desenvolvimento de infra e orquestração do ambiente de demonstração.
- Vinicius Brito: pipeline de processamento de dados e análise.

Cada membro é responsável por manter a evidência atualizada relativa à sua área antes do ensaio final.

## Passo a passo da demonstração (runbook conceitual)
Objetivo: executar uma demonstração repetível e previsível em stand.
1. Preparação: validar ambiente local e confirmar amostras disponibilizadas para demo.
2. Inicialização do fluxo: disponibilizar a interface de registro para atendimento.
3. Registro de caso: simular a entrada de um atendimento com dados do paciente e sintomas.
4. Processamento: disparar o fluxo de processamento para transformar e validar o registro.
5. Consulta do profissional: acessar o perfil do paciente e as anotações geradas.
6. Sugestão analítica: acionar o módulo de apoio à interpretação e exibir resultados com contexto e limitações.
7. Encerramento: coletar evidências (logs de execução, telas e relatório resumido) para anexar à entrega.
Cada etapa deve ser cronometrada e ensaiada para manter previsibilidade.

## Governança de dados, privacidade e retenção
Princípios adotados:
- Minimização: coletar apenas o necessário para fins acadêmicos.
- Transparência: documentar finalidade, gerenciamento e direitos dos titulares.
- Anonimização e pseudonimização: aplicar sempre que necessário para demonstração pública.
Prazos recomendados em contexto acadêmico:
- Registros brutos: retenção limitada a 6 meses, salvo justificativa acadêmica.
- Conjuntos processados e agregados: retenção até 12 meses para reproducibilidade.
- Logs e backups operacionais: retenção de curto prazo para auditoria, sugerida 90 dias.
Procedimento de descarte: documentação das operações de remoção e justificativa para exceções.

## Critérios de avaliação e métricas operacionais
Para a banca, focar nos seguintes critérios:
- Reprodutibilidade: capacidade de executar o fluxo com os artefatos fornecidos.
- Qualidade de dados: completude, consistência e regras de validação documentadas.
- Rigor metodológico: clareza na engenharia de atributos, critérios de validação e avaliação do módulo analítico.
- Transparência e ética: documentação de limitações, vieses e tratamento de dados pessoais.
Métricas operacionais relevantes:
- Tempo de execução do fluxo de demonstração.
- Taxa de conformidade com regras de qualidade definidas.
- Métricas resumidas do módulo analítico com indicação de limites estatísticos.

## Como contribuir e processo colaborativo
Princípios de colaboração:
- Cada contribuição deve vir acompanhada de documentação sucinta sobre a alteração e impacto na demonstração.
- Revisão entre pares para alterações que afetem o fluxo reproducível e a privacidade dos dados.
- Testes mínimos: provisão de casos de teste que permitam validar o fluxo básico da demonstração.
Comunicação interna: centralizar decisões que afetem escopo da apresentação para evitar retrabalho.

## Roadmap pós-expo
Prioridades imediatas após entrega:
- Receber e incorporar feedback da banca.
- Melhorar coleta estruturada de sintomas para reduzir ruído textual.
Médio prazo:
- Aprofundar avaliação do módulo analítico e mitigações de viés.
- Preparar versão para publicação acadêmica com registro de versão dos artefatos.
Longo prazo:
- Estender escopo para múltiplas unidades e instrumentar monitoramento de produção.

## Contatos
Coordenador de documentação e apresentação: Éverson Filipe Campos da Silva Moura  
Para comunicações sobre metodologia e análises: Kaiky Cabral  
Para suporte técnico e execução de demos: Junior e Vinicius Brito

---

### Notas finais
- Este README tem propósito acadêmico e operacional. Priorize clareza documental, evidência reprodutível e preparação controlada da demonstração para maximizar aproveitamento na avaliação.
