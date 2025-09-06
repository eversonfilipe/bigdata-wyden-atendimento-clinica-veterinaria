# BRIEFING DE MVPs — VetCare BigData
Análise profunda e direcionada para desenvolvimento. Objetivo: entregar valor incremental, replicável e auditável para a apresentação acadêmica. Cada etapa abaixo é um MVP independente e cumulativo. Priorize simplicidade, previsibilidade e evidência reproducível.

---

## Princípios orientadores
- Entrega incremental: cada MVP deve ser executável isoladamente e demonstrável ao vivo.
- Reprodutibilidade: scripts para levantar ambiente, gerar dados de exemplo, executar ETL e iniciar API.
- Privacidade primeiro: tratar owner_name / owner_contact como PII; demonstrar pseudonimização em demos públicas.
- Observabilidade mínima: logs estruturados, erros rastreáveis e evidência de execução (artefatos gerados).
- Pragmatismo técnico: soluções que funcionem em ambiente local para apresentação.

---

## MVP 1 — Registro mínimo e API de demonstração
Escopo: capturar atendimentos, armazenar raw, expor API mínima para criar e consultar registros.

Requisitos funcionais
- Endpoint POST /visits que aceita payload com campos mínimos:
  - visit_id (UUID gerado pelo sistema)
  - pet_name
  - pet_age_months
  - owner_id ou owner_name (owner_contact opcional; marcar como PII)
  - breed
  - reported_symptoms (texto livre)
  - visit_timestamp (ISO8601)
- Endpoint GET /pets/{pet_id} que retorna histórico básico (visits list).
- Validação básica do payload e respostas HTTP apropriadas (201, 400, 404).
- Persistência em formato raw (NDJSON/JSON por registro) em diretório versionado para demo.
- Script para gerar 200-500 registros sintéticos de amostra.

Requisitos não funcionais
- Entrada idempotente: mesmas requests com mesmo visit_id não duplicam.
- Logging mínimo: request id, status, erros.
- Tempo de resposta aceitável para demo: latência percebida baixa.
- Arquivo .env.example para variáveis sensíveis; não commitar credenciais.

Observações e riscos
- Tratar owner_contact como campo sensível; oferecer flag de pseudonimização ao salvar (hash ou token).
- Design da API deve permitir fácil extensão para /diagnosis-suggestions no MVP 3.
- Dono da entrega: Junior (implementação API) com suporte de Vinicius (persistência e scripts).

Critérios de aceitação
- POST /visits aceita e persiste registros de teste.
- GET /pets/{id} retorna histórico consistente.
- Script de amostra gera dataset em data/sample_pet_visits.csv ou equivalente.

Entregáveis mínimos
- Código da API + schemas de request/response.
- Diretório data/raw com amostras.
- Script de seed de dados.
- README curto com comandos de demo.

---

## MVP 2 — Ingestão e ETL batch simples (raw -> curated)
Escopo: transformar registros raw em conjunto processado e validado pronto para análise.

Requisitos funcionais
- Job batch que consome arquivos raw e produz dataset processado (formato columnar).
- Normalizações básicas:
  - padronizar timestamps para timezone única
  - normalizar idade em meses
  - limpar textos (trim, remoção de control chars)
  - canonicalizar campos categóricos simples (ex: breed)
- Especificação de schema (arquivo de referência) para visitas e pets.
- Regras de qualidade (checks) para:
  - campos obrigatórios presentes
  - valores racionais para idade
  - timestamps plausíveis
- Logs de transformação com contagem de registros input/output e erros.

Requisitos não funcionais
- ETL idempotente: reprocessar o mesmo raw não gera duplicatas.
- Particionamento lógico por data de visita (para demo local, pasta por date).
- Produzir relatório de qualidade (simple JSON) ao final do job.

Observações e riscos
- Implementar tratamento explícito para registros com campo owner_contact (pseudonimizar antes de deixar em curated se necessário).
- Documentar transformações aplicadas (data dictionary).
- Dono da entrega: Vinicius (ETL) com apoio de Junior (integração I/O).

Critérios de aceitação
- Arquivos curated gerados para uma execução de exemplo.
- Relatório de qualidade indicando percentuais de conformidade.
- Schema de saída documentado.

Entregáveis mínimos
- Script/Job ETL e instruções de execução.
- data/curated com dataset sample.
- data_dictionary.md e logs de execução.

---

## MVP 3 — Modelo baseline de sugestão diagnóstica e serving
Escopo: treinar modelo assistivo simples e integrar endpoint de inferência para demonstração.

Requisitos funcionais
- Pipeline de treinamento que consome curated e produz artefato de modelo versionado com metadata (versão, dataset hash, métricas).
- Modelo baseline:
  - abordagem conservadora e explicável (ex: vetorização de texto + classificador simples)
  - saída: top N sugestões com score/confiança
- Endpoint POST /diagnosis-suggestions que recebe visit_id ou texto de sintomas e retorna sugestões com metadados (versão do modelo, métricas resumidas).
- Model card mínimo descrevendo limitações, viés e uso pretendido.

Requisitos não funcionais
- Inferência determinística para mesma entrada e versão de modelo.
- Tempo de resposta viável para demo.
- Separação entre API de registro e serviço de inferência (mesmo processo ou processo adjacente).

Observações e riscos
- Risco de overclaim: sempre apresentar sugestões como auxílio, não diagnóstico final.
- Dataset sintético limita validade do modelo; documentar claramente no model card.
- Prever mecanismo para desabilitar sugestão no modo apresentação se necessário.
- Dono da entrega: Kaiky (modelagem) + Vinicius (treino) + Junior (serving).

Critérios de aceitação
- Modelo treinado com artefatos versionados.
- Endpoint de inferência responde e retorna top N com scores.
- model_card.md presente e anexado ao relatório técnico.

Entregáveis mínimos
- scripts/train_model.py e artifacts/model_v1 + metadata.json
- endpoint funcionando integrado à API de demonstração
- notebook de avaliação resumido

---

## MVP 4 — Demo reproduzível, QA e documentação final
Escopo: empacotar tudo para apresentação pública, incluindo roteiro, documentação e controles de privacidade.

Requisitos funcionais
- Script único de bootstrap e run_demo_local.sh que:
  - instancia ambiente local (containers ou processos)
  - injeta dados de exemplo
  - executa ETL e registra modelo treinado
  - inicia API e endpoint de inferência
- Runbook passo a passo para apresentador com fallback plan.
- Documentos finais: technical_report.pdf, slides e roteiro de 3 minutos.
- Implementar checks finais: teste smoke que valida endpoints e presença dos artefatos.

Requisitos não funcionais
- Checklist de privacidade: exportações de demonstração devem conter apenas dados pseudonimizados.
- Testes automatizados mínimos (unit + integração smoke).
- CI mínima que roda linters e testes (opcional local para equipe).

Observações e riscos
- Ter fallback offline (vídeo gravado) caso demo ao vivo falhe.
- Ensaio com responsável pela apresentação obrigatório.
- Dono da entrega: Éverson (documentação/coordenação) coordena integração entre membros.

Critérios de aceitação
- Um comando reproduz a demo end-to-end em ambiente padrão da banca.
- Slides e relatório prontos e exportados em PDF.
- Checklist de privacidade atendido.

Entregáveis mínimos
- run_demo_local.sh + scripts de bootstrap/seed/cleanup
- technical_report.pdf e slides
- checklist de apresentação e fallback video

---

## Requisitos transversais (aplicáveis a todos os MVPs)
- Tratamento de PII: rotas e logs não expõem owner_contact; exemplos públicos devem usar pseudônimos.
- Controle de versões de artefatos: metadata.json para cada modelo/transformação.
- Documentação mínima por componente: README curto com comando para executar e resultado esperado.
- Tests: cada componente com testes unitários; pipeline com smoke test de integração.
- Código legível e revisões: PRs revisadas por pelo menos um colega antes de merge.

---

## Riscos principais e mitigação rápida
- Dados insuficientes para modelo: usar heurísticas simples e destacar limites em documentação.
- Demo falha ao vivo: criar script de bootstrap e vídeo de backup.
- Exposição de PII: forçar pseudonimização em exports e aplicar checklist antes de qualquer demonstração pública.
- Tempo limitado: priorizar MVP 1 e MVP 4 (demo reproducível) como entregas obrigatórias.

---

## Definição de Done (por MVP) — checklist resumido
MVP 1
- [ ] POST /visits e GET /pets implementados e testados
- [ ] data/raw com amostras geradas
- [ ] script de seed disponível

MVP 2
- [ ] ETL batch executa e gera curated
- [ ] data_dictionary documentado
- [ ] relatório de qualidade gerado

MVP 3
- [ ] Modelo baseline treinado e versionado
- [ ] Endpoint /diagnosis-suggestions funcionando
- [ ] model_card e notebook de avaliação presentes

MVP 4
- [ ] Script one-shot para demo funcional
- [ ] technical_report.pdf e slides finalizados
- [ ] checklist de privacidade e fallback preparado

---

## Alocação rápida de responsabilidades
- Coordenação geral e documentação: Éverson
- Concepção de requisitos e validação clínica conceitual: Kaiky
- Implementação API e serving, integração: Junior
- ETL, processamento de dados e model training: Vinicius
- Integração final e ensaios de demo: todos (responsável: Éverson)

---

Concentre esforços inicialmente em MVP 1 e MVP 4 (demo repetível). MVP 2 e MVP 3 trazem valor analítico, mas não devem comprometer a previsibilidade do stand. Seja pragmático: entregue evidências, documente decisões e mantenha o escopo enxuto.
