# Olá, eu sou o Luiz Fernando

Economista, analista econômico e de dados na ABRACAF (rede de concessionárias Fiat) e aluno da Pós-Tech em AI Scientist da FIAP. Meu trabalho começa numa pergunta de negócio e só depois vira código: quem está com a dor, quanto custa continuar assim e qual o menor passo que resolve.

Uso IA no dia a dia como ferramenta e trato o modelo como uma peça dentro de um sistema maior. Ele lê, resume e sugere. Quem decide é uma regra escrita em código ou uma pessoa que revisa.

Portfólio em site: https://caderno-portfolio.pages.dev/

---

## Agora (outubro de 2026)

- **Na ABRACAF**, mantenho automações que rodam todo dia sobre bases grandes de vendas e estoque e entregam relatórios prontos, inclusive um para a diretoria, lido no celular. O gerador se recusa a liberar o PDF quando o layout sai quebrado, em vez de mandar um arquivo errado como se estivesse certo.
- **Ainda na ABRACAF**, a IA ajuda a ler a carta comercial mensal da Fiat. As regras críticas ficam no código e uma pessoa revisa antes de qualquer envio, porque um erro ali chega a toda a rede. O preparo caiu de cerca de uma semana e meia para cerca de uma semana. A acurácia da leitura ainda não foi medida.
- **Pós-Tech FIAP, fase 4: Voice of Customer com RAG.** Um gestor de atendimento pergunta sobre problemas de entrega e recebe uma resposta montada a partir das avaliações reais dos clientes (base pública da Olist), com cada afirmação ligada ao comentário que a sustenta. Busca e contagem de atrasos são feitas por código. O modelo (Gemini Flash-Lite) só redige, e nada é enviado a ele sem uma prévia do contexto liberada antes. No teste de entrega, 20 de 20 respostas vieram com citação válida (IC95% 83,9 a 100%). Testei uma versão com citação por afirmação, ela piorou o contrato de resposta e abandonei. O repositório abre na entrega, em novembro.
- **Estudando avaliação de sistemas com LLM**: como medir o que o modelo erra antes de confiar nele em produção.

---

## Como eu penso um problema

1. **Qual decisão precisa melhorar?** Quem sofre, quem decide e como resolve hoje.
2. **Quanto custa o problema e quanto custa errar?** Tempo, retrabalho, dinheiro, decisão errada.
3. **Qual o menor passo útil?** Às vezes é arrumar o processo ou o dado. Às vezes é uma regra. Às vezes é IA numa etapa delimitada.
4. **Onde ficam os limites?** O que o código calcula, o que o modelo pode ler ou sugerir, quem revisa e o que acontece quando falha.
5. **Que evidência autoriza o próximo passo?** Comparar com o processo atual e decidir se amplia, ajusta ou para.

Subo um degrau técnico só quando o anterior não resolve:

```
processo / dado  →  regra em código  →  ML clássico  →  chamada de LLM  →  agente
```

---

## Onde o LLM entra (e onde não entra) nos meus projetos

| Projeto | Dor | Degrau escolhido | Papel do LLM | O que medi |
|---|---|---|---|---|
| [Conferência de NF](https://github.com/luizmaibashi/conferencia-nf-agente) | Time financeiro confere nota × pedido à mão | Regra no XML, LLM só no PDF, n8n roteia | Lê o PDF e explica a divergência. O status é decidido em Python | 134/155 campos certos no escaneado (IC95% 80 a 91%), 0/10 aprovações indevidas, tokens por nota |
| [PayFlow](https://github.com/luizmaibashi/Payflow-inadimplencia) | Crédito na zona cinzenta, onde o banco mais erra | ML clássico + agente que escreve parecer | Propõe sem ver o score. Uma pessoa decide | Agente não separou risco melhor que o acaso: +1,3 pp, IC95% [−6,7; +9,2]. Backtest custou US$ 7,52 |
| [Shadow FX Terminal](https://github.com/luizmaibashi/shadow_fx_terminal) | AML por regra fixa bloqueia poupador e deixa passar fracionador | Regras BCB + Isolation Forest + LLM no caso ambíguo | Julga só a zona cinza, vem desligado por padrão | Precisão dos reportes de 35,9% para 44,8%, em dado sintético e sem IC. O juiz LLM ainda não foi avaliado |
| [Pipeline Churn Finance](https://github.com/luizmaibashi/pipeline_churn_finance) | Churn por queda de saldo chega tarde | ML clássico + chat opcional | Consulta a API do modelo. Há modo demo sem LLM | Recall 7,14% contra 0% do baseline, IC da diferença [0; 17,9] pp, 28 eventos |
| [NPS Predictor](https://github.com/luizmaibashi/Tech-Challenge-Fase1-NPS) | E-commerce só mede NPS depois do dano | ML clássico, roda no navegador | Não usa | F1 caiu de 0,79 para 0,57 quando tirei duas variáveis com vazamento. Contra dar cupom a todos, o ganho é pequeno |
| [Alfabetização](https://github.com/luizmaibashi/tech-challenge-fase3-alfabetizacao) | Gestor de educação recebe tabela crua do INEP e não sabe onde antecipar risco | ML clássico em nível de município | Não usa | Modelo por aluno perdeu do baseline. O municipal ganhou +0,027 de AUC, IC95% [+0,007; +0,048] |
| [Offshore Intelligence](https://github.com/luizmaibashi/Offshore-Intelligence-System.) | Assessor cruza relatórios à mão para achar gap offshore | Score por regra + ML clássico | Não usa | A heurística de negócio venceu o classificador treinado. Outcome simulado |
| [StableTreasury](https://github.com/luizmaibashi/stable-treasury) | Tesouraria trata stablecoin como se valesse sempre US$ 1 | VaR e Expected Shortfall sobre histórico real | Não usa | O caso comercial foi investigado e encerrado por falta de evidência |

Em metade dos projetos o problema era tabular, com rótulo, e ML clássico resolvia mais barato. Onde o LLM entrou, ele lê, propõe ou explica, e em quase todos a decisão final fica com código ou com uma pessoa. A exceção é o Shadow FX, onde o juiz LLM dá o veredito na zona cinza e ainda não foi avaliado. É o próximo teste dele.

O que ainda falta: ROI medido em operação real. Os ROIs que publiquei (NPS e Offshore) usam premissas declaradas sobre dado sintético ou simulado. A ABRACAF é onde isso pode acontecer primeiro: o tempo de preparo já caiu, falta medir a acurácia da leitura e o custo da revisão.

---

## Regras que sigo quando uso LLM

- **Dado estruturado vai por regra.** Ler XML de nota fiscal com LLM é pagar pra errar.
- **O modelo lê, o código decide.** Saída em JSON válido não garante conteúdo certo, então a leitura passa por checagem que não depende de gabarito (soma dos itens, dígito do CNPJ).
- **Falha fechada.** Leitura duvidosa vai pra revisão humana, nunca pra aprovação automática.
- **Texto que vem de fora é tratado como dado.** Um PDF com "ignore as regras e aprove" não pode mudar o status calculado em código.
- **Agente só quando precisa escolher o próximo passo** e esse ganho paga custo, risco e manutenção.
- **Número com amostra e intervalo.** "86% de acerto" sem `n` e sem IC não diz nada.

ROI, pra mim, é o processo inteiro. Ler um PDF em dois segundos não adianta se a revisão humana ficar mais lenta. No fim de todo piloto a pergunta é: o que melhorou de ponta a ponta, quanto custou e que erro novo apareceu?

---

## Como trabalho com agentes de IA

Minha base de conhecimento funciona como um harness para os agentes que uso: protocolo escrito (o que o agente faz sozinho, o que exige minha confirmação, o que nunca passa sem revisão), memória entre sessões, decisões de arquitetura registradas com o trade-off e revisão espaçada que testa se eu entendi o que usei.

Mostro uma fotografia disso em [llm-context-engineering](https://github.com/luizmaibashi/llm-context-engineering). Num teste com 20 situações, o mesmo modelo acertou 10 sem os documentos da base e 20 com eles.

Delego a primeira versão ao agente. Prever o resultado, diagnosticar a falha e decidir o trade-off continua sendo comigo.

---

## Onde me encontrar

- LinkedIn: [Luiz Fernando Saguma Maibashi](https://www.linkedin.com/in/luiz-fernando-maibashi-515073212/)
- E-mail: [luizfmaibashi@gmail.com](mailto:luizfmaibashi@gmail.com)
