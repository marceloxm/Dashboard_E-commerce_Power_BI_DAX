Dashboard_E-commerce_Power_BI_DAX

Neste desafio foi aplicado as técnicas de transformação de dados com Power BI. 
Foi também criado um calendário de datas por meio de expressões DAX. 

--------------------------

Descrição do Desafio de Projeto:

Utilizaremos a tabela única de Financial Sample para criar as tabelas dimensão e fato do nosso modelo baseado em star schema.

O processo consiste na criação das tabelas com base na tabela original. 
A partir da cópia serão selecionadas as colunas que irão compor a visão da nova tabela. 
Sendo assim, a partir da tabela principal serão criadas as tabelas:

Financials_origem (modo oculto – backup)

D_Produtos (ID_produto, Produto, Média de Unidades Vendidas, Médias do valor de vendas, Mediana do valor de vendas, Valor máximo de Venda, Valor mínimo de Venda)

D_Produtos_Detalhes(ID_produtos, Discount Band, Sale Price, Units Sold, Manufactoring Price)

D_Descontos (ID_produto, Discount, Discount Band)

D_Detalhes (*)

D_Calendário – Criada por DAX com calendar()

F_Vendas (SK_ID , ID_Produto, Produto, Units Sold, Sales Price, Discount Band, Segment, Country, Salers, Profit, Date (campos))

------------------

Foi também criado um calendário de datas por meio de expressões DAX:

Primeiramente foi efetuado uma tabela básica. 
Em seguida, abra o Power BI Desktop e, na faixa de opções Modelagem, clique em Nova Tabela.

Então na barra de fórmulas, insira a seguinte expressão DAX:

Dates  = 
  GENERATE ( 
    CALENDAR ( DATE ( 2014, 1, 1 ), DATE ( 2014, 12, 31 ) ), 
    VAR currentDay = [Date]
    VAR day = DAY( currentDay )
    VAR month =  MONTH ( currentDay ) 
    VAR year =  YEAR ( currentDay )
  RETURN   ROW ( 
    "day", day, 
    "month", month, 
    "year", year )
  )
  
Isso gera uma tabela de data simples. Vamos examinar o que está acontecendo aqui.

A função CALENDAR DAX gera uma tabela com uma lista de datas de 1º de janeiro a 31 de dezembro de 2014.
Definimos variáveis ​​(denotadas por VAR) para capturar detalhes da coluna chamada [Data] que é criada pela função CALENDÁRIO.
A função Return gera uma linha por vez. A linha percorre cada item [Data] na lista que foi criada pela função CALENDÁRIO. 
As variáveis ​​são recalculadas para cada execução de linha.
Nota: Ao criar tabelas DAX como estamos fazendo neste exemplo, a tabela DAX é atualizada apenas quando o relatório é atualizado. 
Portanto, se você quiser que a lista de datas aumente com o tempo, ou usar um NOW () na tabela DAX, 
você precisará agendar atualizações para o relatório do Power BI no serviço PowerBI.com.


