# Luiz Fernando Maibashi

Economista. Coloco IA em processo de negócio só onde ela se paga, e meço antes de confiar.

Sou analista econômico na ABRACAF (rede de concessionárias Fiat) e curso a Pós-Tech AI Scientist da FIAP. Começo pela decisão que precisa melhorar: quem sofre com ela, quanto custa continuar assim e qual o menor passo que resolve. Subo um degrau técnico só quando o anterior não deu conta.

```
processo / dado  →  regra em código  →  ML clássico  →  chamada de LLM  →  agente
```

Portfólio em site: https://caderno-portfolio.pages.dev/

---

## Três trabalhos para começar

**1. Em produção, na ABRACAF.** Mantenho automações que rodam todo dia sobre as bases de vendas e estoque da rede e entregam relatórios prontos, um deles para a diretoria, lido no celular. Se o layout do PDF sai quebrado, o gerador se recusa a liberar o arquivo em vez de mandar um relatório errado como se estivesse certo. A IA também ajuda a ler a carta comercial mensal da Fiat. As regras críticas ficam no código e uma pessoa revisa antes de qualquer envio, porque um erro ali chega à rede inteira. O preparo caiu de cerca de uma semana e meia para cerca de uma semana. A acurácia da leitura ainda não foi medida e é a próxima coisa que vou medir. Não tem repositório porque o dado é da empresa.

**2. [Conferência de nota fiscal × pedido](https://github.com/luizmaibashi/conferencia-nf-agente).** O time financeiro confere à mão cada nota contra o pedido de compra. XML vai por regra, porque já é estruturado. O LLM entra só na nota em PDF ou escaneada, e mesmo ali só lê: quem decide o status é o código, e leitura duvidosa vai para uma pessoa. No escaneado, 134 de 155 campos vieram certos (IC95% 80 a 91%), com 0/10 aprovações indevidas.

**3. [RAG sobre avaliações de clientes](https://github.com/luizmaibashi/voc-intelligence-rag-olist)** (Tech Challenge Fase 4, FIAP). Um gestor de atendimento pergunta sobre problemas de entrega e recebe uma resposta montada com comentários reais da base pública da Olist, cada um citado. Busca, filtros e contagem de atrasos são código. O modelo só redige, e só depois que a pessoa lê e libera o contexto. Nos 10 primeiros resultados da busca, 0,71 são relevantes (IC95% 0,55 a 0,86, 14 perguntas, um anotador). Testei duas melhorias, busca híbrida e citação por frase, e abandonei as duas porque pioraram o resultado.

---

## Quando a IA não era a resposta

- **[Raio-X da Carteira](https://github.com/luizmaibashi/raio-x-carteira)** (Hack Brasil 2026). Nenhum número da simulação tributária sai do LLM. Ele só escreve a explicação, e um verificador descarta o texto que cita número fora do cálculo. A conta bate com as calculadoras oficiais da Receita em 19 de 19 casos.
- **[PayFlow](https://github.com/luizmaibashi/Payflow-inadimplencia).** Um agente que escrevia parecer de crédito não separou risco melhor que o acaso: +1,3 pp, IC95% de -6,7 a +9,2, em 564 casos. Custou US$ 7,52 descobrir isso, e por causa desse resultado não construí a tela de produção.
- **[Shadow FX Terminal](https://github.com/luizmaibashi/shadow_fx_terminal).** Na detecção de lavagem com stablecoin, a regra sozinha pegou 1.314 de 1.315 transações de fracionador. O modelo de anomalia não somou nada, e o juiz LLM receberia 25,8% dos casos, contra 0,2% previstos no desenho. O dado é sintético e o teste é circular, e isso está escrito lá.
- **[Offshore Intelligence](https://github.com/luizmaibashi/Offshore-Intelligence-System).** A heurística de negócio venceu o classificador treinado.

Quase todo projeto meu tem um resultado que não se sustentou quando testei, e ele está publicado. Acho que isso diz mais sobre como eu trabalho do que uma lista de acertos.

---

## Como trabalho com agentes de IA

Minha base de conhecimento funciona como um harness para os agentes que uso: protocolo escrito (o que o agente faz sozinho, o que pede minha confirmação, o que nunca passa sem revisão), memória entre sessões, decisões registradas com o trade-off e revisão espaçada que testa se eu entendi o que usei.

Uma fotografia disso está em [llm-context-engineering](https://github.com/luizmaibashi/llm-context-engineering). Num teste com 20 situações, o mesmo modelo acertou 10 sem os documentos da base e 20 com eles.

O agente escreve a primeira versão. Prever o resultado, achar a falha e decidir o trade-off fica comigo.

---

<details>
<summary><strong>Todos os projetos: dor, degrau escolhido e o que medi</strong></summary>

| Projeto | Dor | Degrau escolhido | Papel do LLM | O que medi |
|---|---|---|---|---|
| [Conferência de NF](https://github.com/luizmaibashi/conferencia-nf-agente) | Time financeiro confere nota × pedido à mão | Regra no XML, LLM só no PDF, n8n roteia | Lê o PDF e explica a divergência. O status é decidido em Python | 134/155 campos certos no escaneado (IC95% 80 a 91%), 0/10 aprovações indevidas, tokens por nota |
| [RAG de avaliações (TC4)](https://github.com/luizmaibashi/voc-intelligence-rag-olist) | Gestor de atendimento não sabe de onde vem o resumo que lê | Busca e contagem por código, LLM só redige | Redige com citação, depois de a pessoa liberar o contexto | Precisão@10 0,71 (IC95% 0,55 a 0,86, n = 14). Busca híbrida medida e descartada (0,71 para 0,64) |
| [Raio-X da Carteira](https://github.com/luizmaibashi/raio-x-carteira) | Prestador do Simples não sabe se vale recolher IBS/CBS por fora | Cálculo determinístico com premissa citada | Só escreve a explicação; número fora do cálculo descarta o texto | 19/19 casos conferem com as calculadoras da Receita, 120 testes |
| [PayFlow](https://github.com/luizmaibashi/Payflow-inadimplencia) | Crédito na zona cinzenta, onde o banco mais erra | ML clássico + agente que escreve parecer | Propõe sem ver o score. Uma pessoa decide | Agente não separou risco melhor que o acaso: +1,3 pp, IC95% [-6,7; +9,2]. Backtest custou US$ 7,52 |
| [Shadow FX Terminal](https://github.com/luizmaibashi/shadow_fx_terminal) | AML por regra fixa trava poupador junto com fracionador | Regras BCB + Isolation Forest + LLM no caso ambíguo | Julga a zona cinza, vem desligado por padrão | Regra de comportamento sozinha: 99,0% de precisão (IC95% 98,3 a 99,4). Modelo sem ganho. Zona cinza 25,8% contra 0,2% do desenho. Dado sintético |
| [Pipeline Churn Finance](https://github.com/luizmaibashi/pipeline_churn_finance) | Churn por queda de saldo chega tarde | ML clássico + chat opcional | Consulta a API do modelo. Há modo demo sem LLM | Recall 7,14% contra 0% do baseline, IC da diferença [0; 17,9] pp, 28 eventos |
| [NPS Predictor](https://github.com/luizmaibashi/Tech-Challenge-Fase1-NPS) | E-commerce só mede NPS depois do dano | ML clássico, roda no navegador | Não usa | F1 caiu de 0,79 para 0,57 quando tirei duas variáveis com vazamento. Contra dar cupom a todos, o ganho é pequeno |
| [Alfabetização](https://github.com/luizmaibashi/tech-challenge-fase3-alfabetizacao) | Gestor de educação recebe tabela crua do INEP e não sabe onde antecipar risco | ML clássico em nível de município | Não usa | Modelo por aluno perdeu do baseline. O municipal ganhou +0,027 de AUC, IC95% [+0,007; +0,048] |
| [Offshore Intelligence](https://github.com/luizmaibashi/Offshore-Intelligence-System) | Assessor cruza relatórios à mão para achar gap offshore | Score por regra + ML clássico | Não usa | A heurística de negócio venceu o classificador treinado. Outcome simulado |
| [StableTreasury](https://github.com/luizmaibashi/stable-treasury) | Tesouraria trata stablecoin como se valesse sempre US$ 1 | VaR e Expected Shortfall sobre histórico real | Não usa | O caso comercial foi investigado e encerrado por falta de evidência |

</details>

<details>
<summary><strong>Regras que sigo quando uso LLM</strong></summary>

- **Dado estruturado vai por regra.** Ler XML de nota fiscal com LLM é pagar pra errar.
- **O modelo lê, o código decide.** Saída em JSON válido não garante conteúdo certo, então a leitura passa por checagem que não depende de gabarito (soma dos itens, dígito do CNPJ).
- **Falha fechada.** Leitura duvidosa vai pra revisão humana, nunca pra aprovação automática.
- **Texto que vem de fora é tratado como dado.** Um PDF com "ignore as regras e aprove" não pode mudar o status calculado em código.
- **Agente só quando precisa escolher o próximo passo** e esse ganho paga custo, risco e manutenção.
- **Número com amostra e intervalo.** "86% de acerto" sem `n` e sem IC não diz nada.

ROI, pra mim, é o processo inteiro. Ler um PDF em dois segundos não adianta se a revisão humana ficar mais lenta. No fim de todo piloto a pergunta é: o que melhorou de ponta a ponta, quanto custou e que erro novo apareceu?

</details>

---

## Onde me encontrar

- LinkedIn: [Luiz Fernando Saguma Maibashi](https://www.linkedin.com/in/luiz-fernando-maibashi-515073212/)
- E-mail: [luizfmaibashi@gmail.com](mailto:luizfmaibashi@gmail.com)
