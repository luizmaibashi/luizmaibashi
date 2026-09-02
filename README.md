# Olá, eu sou o Luiz Fernando

Economista, hoje analista econômico e de dados na ABRACAF (rede de concessionárias Fiat), cursando a Pós-Tech em AI Scientist pela FIAP. Trabalho na fronteira entre modelagem quantitativa e engenharia de machine learning: pipelines, agentes e sistemas que medem o próprio resultado antes de declarar vitória.

O critério que uso em todo projeto abaixo é simples: o que foi medido, com que intervalo de confiança, e o que não se sustentou quando testado. Um projeto que mede e reporta um resultado negativo me diz mais sobre o autor do que um projeto que só reporta acerto.

---

## Projetos em destaque

### [StableTreasury](https://github.com/luizmaibashi/stable-treasury): engenharia de risco para tesouraria em stablecoin

Uma empresa que usa stablecoin como capital de giro precisa separar o saldo exibido na carteira da liquidez que sobra depois de um choque de preço. O Depeg Risk Engine calcula VaR e Expected Shortfall sobre o histórico real de USDC e USDT, em vez de assumir que os dois valem sempre US$ 1. O Rail Comparator simula o custo de trilhos de pagamento alternativos, deixando explícito qual premissa (o spread de Wire, por exemplo) muda a conclusão.

Um caso comercial de pré-pagamento foi investigado dentro do próprio projeto e encerrado por falta de evidência de uma lacuna real frente a bancos e sistemas de tesouraria já existentes. Essa decisão está documentada, não escondida.

**Stack:** Python, Streamlit, SQLAlchemy, Postgres, Docker.

### [Shadow FX Terminal](https://github.com/luizmaibashi/shadow_fx_terminal): compliance AML para stablecoin com contexto macroeconômico

Nasceu de uma pergunta de estatística: o brasileiro que compra USDT está especulando ou se protegendo da desvalorização do Real? A resposta virou a variável que falta na maioria dos sistemas de AML, que olham só o comportamento individual da transação.

O pipeline tem três camadas: regras determinísticas das Resoluções BCB 519 a 521, um Isolation Forest calibrado com um Índice de Risco Fiscal próprio, e um LLM que lê atas do Copom para julgar os casos em zona cinzenta. Medido: a camada de contexto melhora a precisão dos reportes ao COAF de 35,9% para 44,8%. O trade-off, também medido e não escondido, é que o falso positivo em poupador legítimo aumenta entre 2,3 e 3,5 vezes.

**Stack:** Python, Scikit-Learn, FastAPI, Streamlit. Licença MIT.

### [PayFlow](https://github.com/luizmaibashi/Payflow-inadimplencia): previsão de risco de crédito com um resultado negativo investigado até a causa raiz

A Camada 1 treina sobre dado real do Home Credit Default Risk (AUC 0,776). A Camada 2 adiciona um agente de underwriting que nunca vê o score, por desenho de schema. O backtest com poder estatístico (n=564, calculado antes de rodar, não depois) respondeu se o agente separa risco real melhor que o acaso: o intervalo de confiança da separação cruza zero. O agente não discrimina de forma detectável.

Investigar por quê levou a um achado mais específico: dentro da zona cinzenta que o agente avalia, o próprio modelo campeão também perde quase toda capacidade discriminativa (AUC 0,56, intervalo que não contém 0,50). A conclusão não é sobre agentes de LLM decidirem crédito mal, e sim sobre essa fatia do dataset estar genuinamente perto do limite do previsível.

**Stack:** Python, Scikit-Learn, Streamlit, LLM (Gemini/Groq) como agente de underwriting.

### [Offshore Intelligence System](https://github.com/luizmaibashi/Offshore-Intelligence-System.): auditoria de um sistema de ML que não fazia o que dizia fazer

Este projeto começou como auditoria, não como construção. Um sistema de priorização de clientes offshore chegava funcionando, mas com alegações que não batiam com o próprio código: pesos descritos como "calibrados por especialista" sem calibração nenhuma, um teste de hipótese citado como diferença confirmada que na verdade tinha efeito estatístico trivial, e um bug real em que notebook e dashboard calculavam o score do mesmo cliente com fórmulas diferentes.

Onze tickets de investigação e cinco ADRs depois, o sistema faz exatamente o que sempre fez, mas agora dá para provar isso, e cada limitação está declarada em vez de escondida. O deploy também foi endurecido: container roda com usuário não root, imagem pinada por digest.

**Stack:** Python, Scikit-Learn (K-Means), Streamlit.

---

## Como penso IA e trabalho com uma base de conhecimento

Não uso um agente de IA como autocomplete. Uso como um harness: um sistema com protocolo escrito (o que o agente decide sozinho, o que exige minha confirmação, o que nunca é feito sem revisão), memória que persiste entre sessões e um conjunto de gates automáticos que rodam antes de qualquer código não trivial ser aceito.

Minha base de conhecimento pessoal é esse harness. Ela guarda o protocolo de engenharia (quando abrir um ADR, quando exigir uma spec antes de aceitar código gerado por um agente), o histórico de decisão de cada projeto, e um mecanismo de revisão espaçada que sabatina se eu de fato entendi um conceito técnico que usei, não só se ele está documentado em algum lugar.

Todo código não trivial gerado por agente passa por revisão de diff antes de virar parte de um projeto, e toda decisão de arquitetura vira ADR com o trade-off explícito, não só o resultado escolhido. A regra que mais aplico é simples: delego a geração da primeira versão, nunca delego o entendimento do porquê ela funciona.

---

## Onde me encontrar

- LinkedIn: [Luiz Fernando Saguma Maibashi](https://www.linkedin.com/in/luiz-fernando-maibashi-515073212/)
- E-mail: [luizfmaibashi@gmail.com](mailto:luizfmaibashi@gmail.com)
