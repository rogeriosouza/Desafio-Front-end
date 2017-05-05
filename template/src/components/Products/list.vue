< Q-data-table
  : Data = "tabela"
  : Config = "config"
  : Columns = "columns"
  @ Refresh = "atualizar"
>
  <! - Representante personalizado para a coluna "mensagem" ->
  < Template  slot = "col-message"  scope = "cell" >
    < Span  class = "light-paragraph" > {{cell.data}} </ span >
  </ Template >
  <! - Representante personalizado para a coluna "fonte" ->
  < Template  slot = "col-source"  scope = "cell" >
    < Span  v-if = "cell.data === 'Auditoria'"  class = "label text-white bg-primary" >
      Auditoria
      < Q-tooltip > Alguns dados </ q-tooltip >
    </ Span >
    < Span  v-else  class = "rotulo texto-branco bg-negativo" > {{cell.data}} </ span >
  </ Template >
  <! - Representação personalizada quando o usuário selecionou uma ou mais linhas ->
  < Template  slot = "selection"  scope = "selection" >
    < Button  class = "clear primário" @ click = "changeMessage (seleção)" >
      < I > editar </ i >
    </ Button >
    < Button  class = "clear primário" @ click = "deleteRow (seleção)" >
      < I > excluir </ i >
    </ Button >
  </ Template >
</ Q-data-table >