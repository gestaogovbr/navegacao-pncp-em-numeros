# História consolidada v2 — Compras publicadas no PNCP

> Status: preliminar. Versão 2 da narração, organizada em blocos, integrando o conceito de compras publicadas, a governança analítica do recorte e o detalhamento itemizado.

## Bloco 1 — Compras publicadas: conceito e contabilização

Tudo começa quando uma contratação pública nasce em um portal de compras, como o `compras.gov.br`. Quando esse registro é gerado no portal de origem — seja licitação, dispensa ou inexigibilidade —, o sistema o envia ao PNCP por API REST. Esse envio marca o início da vida pública da contratação. O fluxo macro, portanto, é simples: portal de origem → API REST → PNCP.

Mas nem todo registro que chega ao sistema representa, de fato, uma contratação válida para análise. Pode haver erro operacional ou falha sistêmica sem qualquer relação com o fato administrativo. Nesses casos, o dado não deve compor a métrica final pública e pode ser excluído logicamente da visão consolidada. Ainda assim, ele não some: permanece preservado para auditoria e rastreabilidade.

Com o processo andando, entra um marco essencial: a data de publicação. É ela que define quando a contratação passa a valer no painel e orienta os recortes temporais da análise. Quando se fala em compra publicada, fala-se de uma intenção formal, de um ato administrativo de contratar um bem ou serviço — o que não significa, por si só, execução integral do gasto.

Vale lembrar que essa publicação não é apenas uma boa prática, é uma obrigação legal. A Lei nº 14.133/2021 estabelece, no Art. 54, que a publicidade do edital de licitação será feita no PNCP; no Art. 94, determina a obrigatoriedade de divulgação no PNCP de contratos e aditamentos; e, no Art. 174, institui o PNCP como o site oficial de divulgação centralizada e obrigatória das contratações públicas. O PNCP é, portanto, o canal oficial — e a publicação no portal é o que dá eficácia pública ao ato.

Também existem estados jurídicos diferentes para uma contratação. Ela pode estar publicada e válida, mas pode ser revogada por conveniência administrativa, anulada por vício ou ainda estar suspensa, situação em que seus efeitos ficam temporariamente sustados até decisão posterior. Para a métrica oficial de compras publicadas, considera-se o registro em estado **publicado no PNCP**; revogadas, anuladas e suspensas não devem compor a contagem final do indicador, sendo necessário aplicar apenas o filtro **Divulgado no PNCP**. Mesmo assim, precisam continuar visíveis em painéis de transparência, porque são parte do histórico auditável e do controle social. Para um detalhamento de cada estado e das transições possíveis, a referência é a seção 5.5 — Situação da Contratação, do Manual de Integração do PNCP.

A partir dessa base, surgem as métricas oficiais: contar contratações em estado publicado, organizar a leitura por exercício (2022, 2023, 2024, 2025) e respeitar os marcos de publicação como eixo temporal. O filtro geral, neste primeiro bloco, é claro: divulgado no PNCP e ano de referência, sob a base normativa da Lei 14.133/2021.

Na prática estatística, aparece outro cuidado importante: os outliers. São contratações com valores extremamente fora do padrão e capazes de distorcer análises. Compras acima de **R$ 8 bilhões** são marcadas com flag booleana (por exemplo, `is_outlier = true`) e devem ser desconsideradas nas métricas oficiais, para evitar ruído e preservar a qualidade analítica.

## Bloco 2 — Filtros secundários da contratação

Com os filtros gerais estabelecidos, a narrativa avança para os filtros secundários, que permitem segmentar a leitura analítica em eixos relevantes.

O **tipo de benefício** aparece como primeiro eixo: participação exclusiva para MPE, cota reservada para MPE, subcontratação ou ausência de benefício.

Em seguida, o **instrumento convocatório**: edital, ato que autoriza a contratação, edital de chamamento, aviso de contratação e outros instrumentos previstos.

O **critério de julgamento** organiza a lógica decisória da disputa: menor preço, maior desconto, melhor técnica ou técnica e preço.

A **modalidade da contratação** abrange pregão, concorrência, dispensa, credenciamento, concorrência presencial e demais modalidades previstas em lei.

Por fim, o **modo de disputa** distingue: não se aplica, aberto, aberto/fechado, fechado/aberto, totalmente fechado e dispensa com disputa.

Para que a consolidação estatística seja confiável, é preciso atenção à qualidade dos dados: rótulos devem ser normalizados antes de contar e comparar — considerando sinônimos, variações textuais e diferenças de caixa.

## Bloco 3 — Recorte analítico do universo observado

Com a base oficial definida e os filtros secundários mapeados, a pergunta central do painel deixa de ser apenas *o que existe no PNCP* e passa a ser *qual conjunto será observado em cada leitura*.

A **regra-mãe do recorte temporal** é que o tempo deve ser definido pela data de publicação no PNCP. A aplicação prática se dá por ano, por mês dentro do ano, e, quando necessário, por comparação mês a mês ou acumulado do exercício. Não se usam, neste painel, data de assinatura, de homologação ou de execução como eixo principal — a entrada estatística oficial da compra ocorre pela publicação.

Antes de descer ao nível local, é preciso construir um **recorte macro**. Os eixos prioritários são esfera administrativa, poder, unidade federativa, região geográfica e, quando disponível, a natureza mais ampla do ente. O objetivo é entender o volume estrutural do PNCP antes de entrar em órgão, unidade ou município, evitando leitura distorcida por começar direto pelo micro-universo.

Depois do corte macro, a análise pode ser afunilada para a realidade operacional específica — o **micro-universo local**. Os eixos prioritários são órgão, unidade compradora, município, entidade vinculada e, quando necessário para desambiguação, o CNPJ do ente. Em outras palavras: primeiro o macro, depois o micro, e só então os filtros secundários.

A **ordem operacional de aplicação dos filtros**, portanto, fica:

1. estado oficial da compra = publicado no PNCP;
2. período por data de publicação;
3. recorte macro;
4. recorte micro;
5. filtros secundários da contratação;
6. exclusão de outliers;
7. cálculo dos indicadores finais.

Essa sequência reduz ruído analítico e melhora a rastreabilidade da consulta.

A **higiene da base**, antes da leitura final, deve excluir ou sinalizar claramente: registros revogados, anulados, suspensos, registros com erro operacional conhecido, outliers acima de R$ 8 bilhões e duplicidades textuais ou cadastrais. Quando a exclusão física não for possível, deve existir flag lógica que retire esses itens da métrica oficial.

Ao final deste bloco, o painel passa a responder com consistência: qual período está sendo observado, qual universo macro foi selecionado, qual micro-universo está dentro do recorte, quais filtros secundários foram aplicados e quais itens ficaram fora da métrica oficial.

## Bloco 4 — Filtros especiais derivados dos itens

Ainda no contexto das compras publicadas, existe uma camada analítica que não nasce apenas da contratação em si, mas dos **itens** que a compõem. Uma compra pode ter um único item ou múltiplos itens, e parte relevante da inteligência do painel depende de filtros que vêm do nível do item, e não apenas do cabeçalho da contratação.

A contratação continua sendo a unidade principal de publicação, mas o item passa a ser a unidade complementar de detalhamento. Quando a pergunta exige precisão material, econômica ou regulatória, a leitura deve descer ao nível do item.

No nível do item, a primeira distinção é a **natureza**: material ou serviço. Esse filtro permite separar comportamentos analíticos diferentes entre aquisição de bens e contratação de serviços.

Além dos benefícios já observáveis no plano geral da contratação, o item pode carregar **tratamento específico**: benefício fiscal próprio ou tratamento favorecido para MPE/MPP, conforme a modelagem disponível na base. É importante separar claramente o benefício do item do benefício geral da contratação quando ambos coexistirem.

O item também pode estar sujeito a **políticas especiais**, como a margem de preferência. Essas políticas devem ser tratadas como filtros próprios, e sua incidência precisa ser mensurada no nível do item, porque nem sempre contaminam a contratação inteira de forma homogênea.

Em determinadas contratações, o **critério de julgamento** também precisa ser observado no detalhamento do item — menor preço, maior desconto, técnica e preço, entre outros — para verificar se a estrutura decisória da disputa se reproduz integralmente no item ou se há particularidades na composição interna da compra.

Há ainda um filtro bastante específico: **patrimônio**. Aplica-se especialmente a leilões, dialoga com receitas e não com despesas, e, por isso, sua leitura não deve ser misturada automaticamente ao mesmo tratamento estatístico das compras correntes. Quando o item estiver marcado por patrimônio, o painel precisa reconhecer um fluxo apartado da lógica tradicional de despesa pública.

Outro marcador relevante é o **orçamento sigiloso**, que afeta a transparência observável do item, influencia a leitura comparativa de valor e exige cuidado para não inferir ausência de informação onde existe apenas restrição de exposição.

Por fim, o item carrega **classificações estruturantes**: código NCM, código NBS, código do item em catálogo específico e categoria. Esses atributos permitem agrupar itens por natureza econômica, comparar famílias de bens e serviços, mapear concentração temática da contratação e construir recortes por catálogo, classe ou segmento.

Para o painel ficar consistente, os filtros derivados dos itens devem obedecer a uma modelagem separada mas vinculada à contratação: manter identificador da compra, manter identificador do item, vincular os filtros do item ao registro da contratação e permitir agregação em dois níveis — contratação e item.

## Encerramento do ciclo — Contratações publicadas

Com este conjunto de blocos, fica fechado o núcleo conceitual e operacional de contratações publicadas no PNCP. A narrativa amadureceu em três camadas:

1. **Camada conceitual** — define o que é a compra publicada e seu marco oficial no PNCP, incluindo a base legal e os estados jurídicos relevantes.
2. **Camada de recorte e governança analítica** — define período, universo, exclusões, filtros de sistema, recorte macro e micro.
3. **Camada de detalhamento itemizado** — incorpora a leitura fina dos itens, seus benefícios, políticas, classificações e marcadores específicos.

O resultado prático é uma base suficiente para sair da etapa descritiva e entrar na etapa de mensuração: indicadores executivos, leituras comparativas e visão de painel — quantidade de compras, valor total publicado no recorte, ticket médio, mediana e concentração por modalidade, critério, benefício e ente.

> Observação operacional: documento preliminar atualizado com o fechamento do ciclo de contratações publicadas. A continuidade natural é abrir o próximo bloco, voltado aos indicadores centrais e à leitura executiva do painel.
