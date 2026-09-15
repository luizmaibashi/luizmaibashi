# Olá, eu sou o Luiz Fernando

Economista, hoje analista econômico e de dados na ABRACAF (rede de concessionárias Fiat), cursando a Pós-Tech em AI Scientist pela FIAP. Trabalho na fronteira entre modelagem quantitativa e engenharia de machine learning: pipelines, agentes e sistemas que medem o próprio resultado antes de declarar vitória.

O critério que uso em todo projeto abaixo é simples: o que foi medido, com que intervalo de confiança, e o que não se sustentou quando testado. Um projeto que mede e reporta um resultado negativo me diz mais sobre o autor do que um projeto que só reporta acerto.

Portfólio em site : https://caderno-portfolio.pages.dev/
---

## Projetos em destaque

### [NPS Predictor AI](https://github.com/luizmaibashi/Tech-Challenge-Fase1-NPS): rastreei um F1 bom demais até a variável errada

O modelo de previsão de NPS bateu 0,79 de F1 na primeira rodada, número bom demais pra ser verdade. Rastreei até achar duas variáveis que só existiam depois da experiência do cliente, e o F1 caiu pra 0,57 sem elas. Numa segunda fase fui além da predição: rodei um experimento causal pra testar se agir sobre essa previsão muda o resultado de verdade, com benchmark de modelos, SHAP e monitor de drift, tudo coberto por 43 testes.

**No ar:** [luizmaibashi.github.io/Tech-Challenge-Fase1-NPS](https://luizmaibashi.github.io/Tech-Challenge-Fase1-NPS/) · **Stack:** Python, Scikit-Learn, CRISP-DM.

### [PayFlow](https://github.com/luizmaibashi/Payflow-inadimplencia): um agente que decide crédito sem ver o score

O agente de LLM deste projeto aprova ou nega crédito sem nunca ver o score do cliente. Rodei um backtest com amostra calculada antes de ver qualquer resultado (n=564) e o veredito não foi o que eu esperava: o agente não separa risco melhor que o acaso. Fui atrás do motivo e achei que o próprio modelo campeão também perde quase toda capacidade de discriminar nessa mesma fatia de dado, então o limite é do dado, não do agente.

**Stack:** Python, Scikit-Learn, Streamlit, LLM (Gemini/Groq).

### [Shadow FX Terminal](https://github.com/luizmaibashi/shadow_fx_terminal): compliance de AML com uma pergunta de macroeconomia dentro

Sistema de compliance pra stablecoin nasceu de uma dúvida de macroeconomia: quem compra USDT no Brasil está especulando ou se protegendo do Real? Testei essa ideia como uma camada extra de contexto no pipeline de AML, ao lado das regras determinísticas do BCB e de um Isolation Forest. Essa camada levou a precisão dos reportes ao COAF de 35,9% pra 44,8%, com o custo em falso positivo de poupador legítimo também medido.

**Stack:** Python, Scikit-Learn, FastAPI, Streamlit. Licença MIT.

### [StableTreasury](https://github.com/luizmaibashi/stable-treasury): engenharia de risco pra quem assume que stablecoin vale sempre US$ 1

Boa parte dos sistemas financeiros trata USDC e USDT como se o preço nunca saísse de US$ 1. Construí um motor que calcula VaR e Expected Shortfall sobre o histórico real dos dois, pra mostrar quanto essa suposição custa quando quebra. No meio do caminho surgiu um caso comercial de pré-pagamento, investiguei e encerrei dentro do próprio projeto por falta de evidência de uma lacuna real.

**Stack:** Python, Streamlit, SQLAlchemy, Postgres, Docker.

### [Tech Challenge Fase 3: Alfabetização](https://github.com/luizmaibashi/tech-challenge-fase3-alfabetizacao): um modelo reprovou, e mudei o grão do problema

O desafio pedia um modelo que prevê alfabetização aluno por aluno. Testei contra o critério de sucesso que eu tinha definido antes de treinar qualquer coisa, e reprovou. Em vez de forçar o resultado, mudei o grão pra priorização municipal, e esse segundo modelo bate o baseline na maior parte dos estados analisados.

**Stack:** Python, Scikit-Learn, SHAP.

### [Pipeline Churn Finance](https://github.com/luizmaibashi/pipeline_churn_finance): churn prediction refeito pra escala institucional

Peguei o mesmo problema de churn e reconstruí pensando em escala de gestora de patrimônio de verdade: PySpark, governança via MLflow, dado sintético tratado com o mesmo rigor de dado real. Pra publicar sem manter servidor no ar, portei o modelo pra rodar dentro do navegador, com 58 testes garantindo que o resultado bate com a versão Python.

**No ar:** [luizmaibashi.github.io/pipeline_churn_finance](https://luizmaibashi.github.io/pipeline_churn_finance/) · **Stack:** Python, PySpark, MLflow, FastAPI, Streamlit.

---

## Como penso IA e trabalho com uma base de conhecimento

Não uso um agente de IA como autocomplete. Uso como um harness: um sistema com protocolo escrito (o que o agente decide sozinho, o que exige minha confirmação, o que nunca é feito sem revisão), memória que persiste entre sessões e um conjunto de gates automáticos que rodam antes de qualquer código não trivial ser aceito.

Minha base de conhecimento pessoal é esse harness. Ela guarda o protocolo de engenharia (quando abrir um ADR, quando exigir uma spec antes de aceitar código gerado por um agente), o histórico de decisão de cada projeto, e um mecanismo de revisão espaçada que sabatina se eu de fato entendi um conceito técnico que usei, não só se ele está documentado em algum lugar.

Todo código não trivial gerado por agente passa por revisão de diff antes de virar parte de um projeto, e toda decisão de arquitetura vira ADR com o trade-off explícito, não só o resultado escolhido. A regra que mais aplico é simples: delego a geração da primeira versão, nunca delego o entendimento do porquê ela funciona.

---

## Onde me encontrar

- LinkedIn: [Luiz Fernando Saguma Maibashi](https://www.linkedin.com/in/luiz-fernando-maibashi-515073212/)
- E-mail: [luizfmaibashi@gmail.com](mailto:luizfmaibashi@gmail.com)
