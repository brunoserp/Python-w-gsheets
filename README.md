# Python e Google Sheets
Suponha que você receba uma planilha com preços da concorrência de setembro com as colunas data | tipo | categoria | preço concorrência | e te peçam para juntar numa outra planilha com dados históricos, com as colunas | tipo | categoria | preço concorrência | preço interno |, tudo no Google Sheets.
Repare que na coluna de setembro falta a coluna de preço interno, que pode ser incluída por uma planilha dimensão com os preços mensais da sua empresa para todos os produtos da concorrência.

![image](https://github.com/user-attachments/assets/43f3594c-03f2-4f57-b0a1-3575b3aa3763)

<hr>
# Como as bibliotecas do Python interagem com o Google Sheets
Uma API é uma forma de permitir que diferentes sistemas se comuniquem entre si. <br>
A biblioteca OAuth 2.0 garante segurança ao acessar conteúdos protegidos, como o Google Sheets, dando acesso à determinada conta sem usar o login e senha. <br>
Uma vez liberado o acesso por meio do OAuth 2.0, o gspread funciona como meio para acessar o Google Sheets. <br>
Essa comunicação se dá por meio de requisições, que são solicitações com padrões definidos. Por exemplo, as requisições GET/POST/PUT são usadas para ler, enviar e atualizar dados, respectivamente. O gspread traduz os comandos do Python para a linguagem própria da requisição.

<hr>
# Caso prático
Para gerar as 3 planilhas citadas, usei o programa 'gerador de planilhas.py'
O programa da automação é o 'gspread_prática.py', que segue o passo a passo:

1) Acesso às 3 planilhas do Google Sheets por meio de uma credencial que do meu e-mail e que permite acesso aos arquivos. Isso é feito por uma biblioteca do Google

A partir daí, todos os passos foram feitos pelo gspread:
2) Extração das informações de cada uma das 3 tabelas
3) Aplicação das fórmulas: primeiramente, um concatenado na planilha dimensão e na de setembro, e depois o PROCX na tabela de setembro puxando o preço interno da tabela dimensão, por meio dos concatenados.

Vale ressaltar que a aplicação das fórmulas foi feita pela função batch_update do gspread, que envia uma única requisição ao API do Google Sheets com a aplicação da fórmula em todas as linhas de uma única vez, melhorando a performance do programa, uma vez que há um limite de requisições por minuto.

4) Colagem dos valores do PROCX e exclusão as colunas concatenadas
5) Junção da tabela de setembro com a tabela com dados históricos.
