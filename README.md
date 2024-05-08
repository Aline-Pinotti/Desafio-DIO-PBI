##### Alguns ajustes necessários para a inclusão da base de dados pelo Azure:
<br>
- Nos arquivo de criação das tabelas, haviam uns delete que não especificavam a deleção da constraint, assim o Bash da Azure procurava uma coluna para deletar. Por isso foi necessário ajustar o script para deletar as constraints.
<br>
- Para popular as tabelas, também foi necessário alguns ajustes, como reordenar os registros em employee, uma vez que estavam sendo incluídos gerentes que ainda não haviam sido cadastrados nas tabelas. Alterei a ordem, para que os gerentes fossem incluídos primeiro.
<br><br>
##### Agora o Power BI:
<br>
- Ao importar os dados do banco de dados na nuvem (criado no Azure), após selecionar todas as tabelas, foi utilizada a opção <i>Transformar Dados</i>, para fazer o devido tratamento.
<br>
- Removidas as colunas que o Power BI cria referente aos relacionamentos com outras tabelas (as necessárias serão inclusas posteriormente no <i>Join/Combinar</i>)
<br>
- Verificados todos os cabeçalhos, tabela por tabela:
  -  Ajustado os nomes das colunas para ficar mais amigável;
  -  Ajustado o tipo de dado da coluna de Salário (única do tipo monetário do schema), na tabela employee (Empregados), para <i>Número Decimal Fixo</i>.
<br>
- Verificado se existem colunas ou linhas nulas. Apenas para supervisor/gerente, na tabela de empregados, mas para um gerente que não tem outro empregado acima. Ou seja, nenhuma informação nula que fosse preciso alguma intervensão.
- Nenhum outro colaborador ou departamento sem gerente.
<br>
- Todos os projetos possuem horas informadas.
<br>
- Para o endereço do empregado, que é uma informação complexa, pois possui a rua (logradouro), número, cidade e UF, todos no mesmo registro:
  -  primeiramente, foram ajustados os endereços, removendo o hífen no nome da rua de um dos endereços, utilizando o recurso <i>Substituir Valores</i> para que ficassem todos padronizados;
  -  finalmente, utilizando do <i>Dividir Coluna > Por Delimitador</i>, o endereço foi separado, pelo delimitador hífen (-), em Logradouro, Número, Cidade e UF.
  <br>
- Foi utilizada a opção de <i>Mesclar Consulta como Nova</i> para associar o nome do departamento ao empregado, e apresentando o nome do Departamento ao consultar o Empregado por essa nova consulta.
  <br>
  * Foi utilizada a opção de Mesclar, para que pudesse apresentar o nome do departamento como nova coluna, e o <i>Tipo de Junção <b>Externa esquerda</b></i> para que todos os registros de empregados fossem listados, uma vez que essa foi selecionada como tabela de referência.
  * Para combinação existem três opções:
    * <b>Mesclar</b>, mencionada acima, que realciona duas ou mais tabelas, contanto que ambas tenha uma informação em comum - como o número do departamento, nesse caso, e que irá trazer novas colunas com as informações relacionadas;
    * <b>Acrescentar</b>, que é utilizada para registros com mesmas colunas, nos quais são inclusas novas linhas/registros/tuplas (não novas colunas) Pr exemplo: se ao importar os dados, trouxéssemos apenas os dados dos Departamentos criados ou iniciados até 2023, e queremos acrescentar os departamentos criados a aprtir de 2024. Essa opção vai adicionar mais registros a essa tabela já carregada;
    * <b>Combinar</b>, na qual é criada uma consulta de dois arquivos (texto, planilha, JSON) diferentes.
<br>
  - Ao extender as informações, apenas foi selecionada a coluna com a descrição do departamento.
<br>
- Na tabela de empregados, foram mescladas as colunas com informações de Nome, Inicial do nome do meio e Sobrenome para uma coluna chamada Nome (apenas).
<br>
- Então foi mesclado também à nova consulta com Empregado e Departamento, o Nome do Supervisor/gerente, assim como feito anteriormente com empregado e departamento (dessa vez sem gerar nova Consulta, resolvi reaproveitar a última consulta gerada na mescla entre empregado e departamento).
<br>
- Foi mesclado também o departamento com alocalização, a fim de de criar uma combinação departamento-local única. <b style="background-color: #66F; font-weight: normal;">Utilizamos o mesclar para juntar as colunas das tabelas - o atribuir incluiria mais informações/registros/tuplas na tabela e o que queremos aqui é a informação de departamento para cada local (ou vice-versa).</b> Após a mescla, as colunas foram combinadas utilizando o hífem como separador.
<br>
- Foi criada uma nova Consulta através da <i>Combinação</i> na tabela Empregados, para juntar cada colaborador com seu gerente e, em seguida, foi agrupado pelo Gerente, por contagem, para definir quantos colaboradores existem por gerente.
<br>
- Por fim, cada Tabela/Consulta foi revisitada, verificando e eliminando as colunas desnecessárias, que não seráo usadas no relatório.
