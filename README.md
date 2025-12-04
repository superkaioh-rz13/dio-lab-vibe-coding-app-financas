# PRD — Aplicativo de Organização de Finanças Pessoais por Conversa
> Versão 1.0 — Documento completo para LOVABLE  
> Linguagem: clara, educativa e acessível (pt-BR)

---

## 1. Contexto
O aplicativo tem como objetivo auxiliar o usuário a organizar suas finanças pessoais utilizando **linguagem natural**, reduzindo fricção no registro de entradas/saídas e promovendo hábitos financeiros mais saudáveis por meio de incentivos visuais, análises automáticas e acompanhamento contínuo.

---

## 2. Problema
Aplicativos financeiros tradicionais possuem interfaces complexas, cheias de passos e pouco convidativas. Isso afasta usuários pouco familiarizados com tecnologia e desestimula uso contínuo.  
A solução proposta é uma **interface conversacional** que simplifica a interação, incentiva hábitos saudáveis e fornece análises que ajudam o usuário a manter uma vida financeira equilibrada.

---

## 3. Público-Alvo
- Usuários de todos os níveis de familiaridade com tecnologia que precisam organizar suas finanças de maneira simples.  
- Usuários mais avançados que desejam dados mais detalhados, gráficos, filtros e controle manual estilo planilha.  

---

## 4. Proposta de Valor
Permitir que qualquer pessoa organize sua vida financeira conversando com o aplicativo, sem precisar entender de planilhas ou navegações complexas — mas ainda mantendo profundidade e ferramentas para quem quiser.

---

## 5. Funcionalidades-Chave (priorização MVP)
### MUST-HAVE (MVP)
1. Registro de entradas e saídas via linguagem natural.  
2. Correção de registros por linguagem natural.  
3. Classificação automática das transações.  
4. Visualização de gráficos básicos atualizados em tempo real (dia/semana/mês/ano).  
5. Resumo do “Agente Financeiro” avaliando a vida financeira do usuário (Desorganizada / Médio / Organizada).  

### SHOULD-HAVE (pós-MVP imediato)
6. Criação/edição de metas financeiras por linguagem natural.  
7. Inserção manual avançada estilo planilha (mais controle).  
8. Recomendações personalizadas a cada novo registro.  

### NICE-TO-HAVE
9. Gamificação visual (badges, níveis, notificações inteligentes).  
10. Exportação/importação de dados (ex.: CSV).  
11. Suporte a múltiplos perfis.  

---

## 6. Regras de Negócio
- Todo registro deve conter: `valor`, `tipo` (entrada ou saída), `categoria`, `data` e `opcional: notas`.  
- Classificação automática deve sempre fornecer uma categoria baseando-se em heurísticas e ML; baixa confiança exige confirmação.  
- Edição de qualquer campo deve atualizar cálculos, gráficos e agregados imediatamente.  
- Histórico deve registrar qualquer alteração feita (auditoria).  
- A avaliação financeira do agente deve ser recalculada ao menos semanalmente ou após volume significativo de inputs.  

---

## 7. Taxonomia Inicial de Categorias
- Alimentação  
- Transporte  
- Moradia  
- Saúde  
- Educação  
- Lazer  
- Assinaturas  
- Investimentos  
- Renda  
- Outros  
*(Categorias adicionais podem ser criadas pelo usuário posteriormente.)*

---

## 8. Modelo de Conversa (NLU)
### Intents principais
- `registro_despesa`  
- `registro_receita`  
- `corrigir_registro`  
- `consultar_resumo`  
- `criar_meta`  
- `editar_categoria`  
- `entrada_planilha`  

### Entities
- `valor`  
- `categoria`  
- `data`  
- `tipo`  
- `nota`  
- `metodo_pagamento` (opcional)  

### Exemplos de frases
- “Gastei R$ 120 no mercado hoje.”  
- “Recebi 900 reais do meu trabalho.”  
- “Corrige: era R$ 150, não 120.”  
- “Quero economizar 500 por mês.”  
- “Mostre meus gastos desta semana.”  

---

## 9. Telas do MVP (alto nível)
1. **Tela Conversacional (principal)**  
   - Campo de mensagem; histórico; atalhos rápidos.  
   - Confirmação de ações e micro-feedback visual imediato.  

2. **Dashboard de Resumo**  
   - Gráfico pizza por categoria (mês atual).  
   - Gráfico de linha dos últimos 30 dias.  
   - Saldo geral + indicadores simples.  
   - Filtros: dia / semana / mês / ano.  

3. **Tela Planilha (manual avançada)**  
   - Grade editável com valor, data, categoria e nota.  

4. **Tela de Metas**  
   - Listagem de metas e progresso.  

5. **Tela de Configurações/Perfil**  
   - Privacidade, exportar dados, preferências.  

---

## 10. Requisitos Técnicos
### Backend
- API REST (Node, Python ou Go).  
- PostgreSQL (com criptografia at-rest).  
- Redis para cache.  
- Serviço de NLU (Rasa, Dialogflow ou LLM com regras).  
- Módulo de agregação para dashboards (via consultas otimizadas ou tabela agregada).

### Frontend
- React Native ou Flutter (mobile-first).  
- Atualização de gráficos em tempo real (< 2s).  

### Segurança (LGPD)
- Consentimento explícito para uso de dados financeiros.  
- Exclusão total dos dados quando solicitado.  
- Logs de auditoria para registros e edições.  

---

## 11. Performance & Observabilidade
- Gráficos devem atualizar em ≤ 2 segundos após novo registro.  
- Log de eventos: `criar_transacao`, `editar_transacao`, `confirmacao`, `ver_resumo`.  
- Monitoramento: Sentry + métricas de API.  

---

## 12. Critérios de Aceite (MVP)
1. Registrar entrada/saída corretamente via linguagem natural em ≥ 90% das frases de teste.  
2. Corrigir registro existente via linguagem natural em ≥ 90% das tentativas.  
3. Classificação automática com acurácia ≥ 80% no conjunto de categorias padrão.  
4. Dashboard atualiza imediatamente após qualquer modificação (≤ 2s).  
5. “Agente Financeiro” gera diagnóstico e 3 recomendações rápidas baseadas nos dados do usuário.  
6. Fluxo conversacional completo (entrada → parse → confirmação → registro) deve ter taxa de sucesso ≥ 85%.

---

## 13. Métricas (KPIs)
- **Retenção**: D7 ≥ 25%, D30 ≥ 15%.  
- **NLU Accuracy**: ≥ 90%.  
- **Tempo médio para registrar**: < 30s.  
- **Conversões**: ≥ 1 registro por semana/usuário ativo.  
- **CSAT/NPS** após 2 semanas: ≥ 4 / ≥ 20.  

---

## 14. Riscos & Mitigações
- **Baixa acurácia do NLU** → confirmação inteligente e fallback para formulário.  
- **Usuários leigos** → micro-copy educativo e exemplos práticos.  
- **Privacidade sensível** → criptografia, LGPD, boa comunicação.  

---

## 15. Plano MVP — Validação Inicial
### Etapa 1 — POC (2 semanas)
- Chat UI + backend simples + parser inicial.  
- Validar: tempo de registro e entendimento do usuário.  

### Etapa 2 — MVP fechado (4–6 semanas)
- Dashboard + correções + classificação automática.  
- Teste com usuários reais; coletar feedback claro.  

### Etapa 3 — Beta público (8–12 semanas)
- Metas + planilha + ajustes na IA.  
- Medir KPIs: retenção, tempo de registro, acurácia.  

---

## 16. Checklist para Desenvolvimento
- [ ] NLU funcional com intents principais.  
- [ ] Estrutura de categorias funcionando.  
- [ ] Registro conversacional completo.  
- [ ] Correção conversacional ativa.  
- [ ] Dashboard com filtros.  
- [ ] Avaliação financeira automática.  
- [ ] Segurança e LGPD.  
- [ ] Logs de auditoria.  
- [ ] Micro-copy revisada.  
- [ ] Testes de usabilidade.  

---

## 17. Entregável esperado pela IA (Lovable)
Gerar:  
- Plano de MVP do aplicativo.  
- Desenho das principais telas.  
- Recursos necessários para implementação.  
- Estratégia inicial de validação.  
Tudo com explicações simples, educativas e diretas.

---
<img width="1303" height="917" alt="image" src="https://github.com/user-attachments/assets/b191ff93-bac4-4acb-80d7-09e1149ba17f" />
<img width="1032" height="858" alt="image" src="https://github.com/user-attachments/assets/7a133363-99ca-48ab-9021-81bd9e6c9abb" />
<img width="1030" height="503" alt="image" src="https://github.com/user-attachments/assets/94b24585-cb25-4ad3-ae3d-4f2d71d37153" />
<img width="1025" height="823" alt="image" src="https://github.com/user-attachments/assets/1aedd517-9f82-4803-a720-0befff783c92" />


