# História consolidada — Compras homologadas no PNCP

> Status: preliminar. Segundo capítulo da narração, na sequência das contratações publicadas. A compra publicada representa a entrada formal do processo no ambiente público; a compra homologada representa um estágio posterior, em que o procedimento já produziu resultado validado pela autoridade competente.

## Bloco 1 — Conceito de compra homologada

Agora que encerramos o ciclo das contratações publicadas, vamos falar sobre contratações homologadas. Como já vimos antes, é preciso entender os filtros aplicados — e parte deles permanece. A compra precisa estar **divulgada corretamente no PNCP**, e isso não muda. Os filtros estruturais da etapa anterior continuam valendo: consistência da base, ingresso pelo PNCP e tratamento de outliers seguem como pré-condições.

A diferença central está no eixo do valor analisado. Na etapa de contratações publicadas, a leitura de outlier incidia sobre o valor estimado da contratação. Na etapa de compras homologadas, o critério passa a observar o **valor efetivamente homologado**, ou seja, o valor resultante do processo competitivo. Em uma frase: antes, outlier era calculado sobre o valor estimado/publicado; agora, sobre o valor homologado/resultante.

E por que essa métrica muda? Porque a compra homologada já está em outra fase do processo administrativo. Ela não é mais lida apenas como intenção pública de contratar, mas como processo que passou pela seleção do fornecedor e alcançou um resultado validado. Pode ter havido disputa, pode ter surgido vencedor ofertando o menor preço ou o melhor preço — e a Lei 14.133/2021 traz várias hipóteses em relação à formação do preço. O valor relevante deixa de ser expectativa inicial e passa a ser o valor produzido pelo resultado homologado.

A compra homologada, portanto, é uma etapa do processo de seleção do fornecedor: demonstra que o procedimento alcançou resultado reconhecido formalmente pela Administração. Sua leitura estatística precisa refletir o desfecho da competição, e não apenas a fotografia inicial da publicação.

## Bloco 2 — Marco temporal da homologação

Se, na contratação publicada, o ano da publicação era o eixo temporal relevante, agora, na homologação, o que passa a importar é o **ano do resultado**. Esse marco é central porque a homologação não deve ser localizada pela data em que a compra foi publicada, mas pela data em que o processo passou a apresentar resultado válido de seleção de fornecedor.

E onde esse marco aparece no painel? Os filtros relacionados ao ano da publicação continuam visíveis nos indicadores, mas, para a leitura de compras homologadas, o recorte principal migra para o **filtro de resultado**. Os campos temporalmente relevantes passam a ser ano, mês e data do resultado.

A regra de formação dessa data é a seguinte: o resultado da compra passa a existir a partir do **primeiro item com resultado** ou com homologação registrada. Se uma compra possui múltiplos itens e apenas um deles já apresenta resultado, a data mínima desse primeiro item passa a ser a data de resultado da compra para fins de contabilização geral. Exemplo prático: uma compra com 10 itens em que apenas 1 já teve resultado homologado é localizada temporalmente pela data desse primeiro resultado.

A justificativa metodológica é encontrar a melhor localização, no espaço e no tempo, das contratações que efetivamente passaram pela seleção de fornecedor. A lógica adotada não exige que todos os itens tenham resultado simultâneo; basta a existência do primeiro item com resultado válido para que o marco temporal seja formado, garantindo regra única de leitura.

Reconhece-se, porém, que esse critério pode sofrer dinamismo ao longo do tempo. Outros itens da mesma compra podem receber resultado posteriormente — a compra entra no recorte pela primeira data de resultado, mas seu conteúdo quantitativo ou financeiro pode evoluir depois, à medida que novos itens são homologados. Essa dinâmica funciona como uma **slowly changing dimension** — em português, transformação lenta da informação ao longo do tempo. Não é o ideal, mas acontece. Na prática, o painel pode, em determinados momentos, mostrar valor ou quantidade ampliados para a mesma compra, porque itens adicionais tiveram resultado em momento posterior.

Recapitulando a regra consolidada deste bloco:

- a compra deve continuar **publicada no PNCP**;
- o recorte temporal deixa de priorizar a data de publicação;
- passam a contar o **ano, o mês e a data do resultado**;
- a data de referência é a do **primeiro item com resultado**;
- a regra de outlier continua aplicada, agora sobre os homologados.

Há, ainda, uma exceção relevante e que pode parecer estranha à primeira vista: um mesmo item pode apresentar **mais de um resultado**. Isso não é erro por definição. A própria Lei 14.133/2021 admite hipóteses excepcionais em que esse comportamento ocorre — para mais detalhes sobre o motivo, a recomendação é consultar a própria lei. Operacionalmente, a existência de mais de um resultado para o mesmo item deve ser tratada como possibilidade normativa, e não como inconsistência automática. Para a localização temporal da compra homologada, permanece válida a regra da primeira data de resultado; resultados posteriores do mesmo item ou de outros itens podem alterar a composição quantitativa ou financeira observada no painel. A consequência analítica é direta: a compra pode continuar evoluindo mesmo após o primeiro resultado capturado, e a leitura de homologados exige cuidado com versões tardias, complementações e efeitos incrementais sobre a métrica.

## Bloco 3 — Filtros do resultado da contratação

A leitura dos **filtros de resultado** exige atenção especial, porque é fonte recorrente de confusão analítica. Esses filtros não devem ser confundidos com os filtros próprios dos itens da contratação. Aqui, o foco deixa de ser a composição interna do item e passa a ser o **resultado produzido pela contratação** em relação ao fornecedor e às condições do resultado homologado.

No nível do resultado, é possível identificar informações diretamente ligadas ao **fornecedor** vencedor ou associado ao desfecho: nome, CPF ou CNPJ, tipo (pessoa física ou jurídica) e natureza jurídica. Esses campos qualificam quem efetivamente aparece vinculado ao desfecho da contratação.

Também aparecem atributos de **origem e procedência** associados ao resultado, como origem do produto e país de origem do fornecedor, quando disponíveis. Esses filtros permitem leitura complementar sobre a composição do resultado homologado.

Outro filtro relevante é o **porte do fornecedor** — MPE, EPP ou demais classificações cabíveis conforme a base disponível. É importante interpretar o porte como atributo do fornecedor que obteve o resultado, e não como simples característica abstrata da contratação.

Um ponto crítico de confusão está na **margem de preferência**. É possível existir indicador de margem de preferência no **item** e também informação de margem de preferência no **resultado**, e a diferença é conceitual. No item, a leitura indica atributo ou previsão associada àquele item; no resultado, a leitura informa que a contratação efetivamente produziu resultado com aplicação da margem de preferência, inclusive com seus efeitos e aplicações concretas. Trocar essas duas leituras gera erro analítico.

A regra de separação, portanto, é clara: filtro do **item** descreve características, condições ou classificações do item licitado; filtro do **resultado** descreve o desfecho da contratação em relação ao fornecedor e às condições efetivamente observadas no resultado homologado. Se essa separação não for respeitada, o painel pode produzir leituras equivocadas — atribuir ao item algo que pertence ao fornecedor vencedor, tratar condição do resultado como se fosse mera característica estrutural do item, ou confundir aplicação efetiva de política pública com simples possibilidade ou marcação prévia.

Em síntese, ao analisar compras homologadas, os filtros de resultado devem ser lidos como camada própria da contratação, voltada a responder: quem venceu, qual fornecedor está associado ao resultado, qual seu porte e natureza, qual a origem vinculada ao resultado e quais políticas — como margem de preferência — efetivamente se materializaram no desfecho homologado.

## Encerramento do capítulo — Compras homologadas

Com este capítulo, fica fechada a transição da etapa de **publicação** para a etapa de **confirmação de resultado**. A leitura analítica passa a se organizar em três pontos:

1. **Continuidade dos filtros estruturais** — divulgação no PNCP, consistência da base e tratamento de outliers seguem valendo, mas o outlier passa a ser calculado sobre o valor homologado.
2. **Novo marco temporal** — o eixo migra da data de publicação para a data do resultado, definida pelo primeiro item homologado, com reconhecimento explícito do efeito *slowly changing dimension* e da hipótese excepcional de item com múltiplos resultados.
3. **Camada de filtros de resultado** — fornecedor, origem, porte e margem de preferência passam a ser leituras próprias do desfecho homologado, separadas dos filtros do item.

> Observação operacional: documento preliminar do segundo capítulo, em sequência ao ciclo de contratações publicadas. A continuidade natural é avançar para os indicadores executivos do painel sobre homologados — quantidade, valor homologado, ticket médio, mediana e concentração por fornecedor, porte, modalidade e ente.
