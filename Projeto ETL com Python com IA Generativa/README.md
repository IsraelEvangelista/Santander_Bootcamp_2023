# Projeto Explorando IA Generativa em um Pipeline de ETL com Python

Entendendo o Desafio
Agora é a sua hora de brilhar e construir um perfil de destaque na DIO! Explore todos os conceitos explorados até aqui e replique (ou melhore, porque não?) este projeto prático. Para isso, crie seu próprio repositório e aumente ainda mais seu portfólio de projetos no GitHub, o qual pode fazer toda diferença em suas entrevistas técnicas 😎

Vocês já mergulharam a fundo no mundo da Ciência de Dados conosco! Juntos, construímos um pipeline ETL eficaz, começando com a simples extração de IDs de usuários de uma planilha, seguindo para uma transformação inovadora com a IA do GPT-4 da OpenAI, e culminando no carregamento desses dados transformados de volta ao 'Santander Dev Week 2023'. Agora, o desafio é reimaginar esse processo de ETL. Como vocês aplicariam o que aprenderam em um novo domínio de aplicação, sem depender diretamente de APIs externas (caso queiram simplificar)? Pensem nas infinitas possibilidades e domínios que podem ser explorados, e deixem a criatividade fluir!

________________________________________________________________________________________________________

# Acesso ao Projeto COLAB

[IA Generativa em um Pipeline de ETL com Python](https://github.com/IsraelEvangelista/Santander_Bootcamp_2023/blob/main/Projeto%20ETL%20com%20Python%20com%20IA%20Generativa/Projeto_ETL_DIO_Santander.ipynb)

## Criação da base de dados usando prompt elaborado com GPT-4 e Code Interpreter

Nesta primeira etapa, optei por usar o poder da IA Generativa para criar um banco de dados que simula o de um banco comercial. Os protagonistas desta etapa foram o GPT-4 e o Code Interpreter. Este último, é uma extensão responsável por permitir que o GPT-4 leia ou gere arquivos. Isso significa que posso joagr um prompt nele, pedindo para analisar um determinado arquivo de dados, por exemplo, e solicitar ao GPT que nos auxilie ou nos dê insights sobre as informações ali presentes. Para este projeto, o Code Interpreter foi usado para gerar três tabelas associadas por uma chave primária, simulando um banco de dados, porém em excel. 

Antes de mais nada, foi rodado um prompt no GPT-4 solicitando para que ele criasse um prompt gerando os parâmetros necessários para as tabelas e que fosse iterando até que eu estivesse satisfeito com o resultado. Mas como assim? 

Basicamente, o prompt cria regras de negócio sobre o contexto solicitado e uma outra camada de regras para que a IA crie o melhor prompt para atender ao resultado do negócio. Segue um exemplo abaixo de como ficaria:

```
Preciso que você elabore um prompt para ser usado aqui mesmo no GPT 4 - Code interpreter, para criação de uma pequena base de dados divididos em três tabelas no contexto de um banco.

[REGRAS DAS TABELAS]
> Use IDs para cadastrar os usuários. Estes serão as chaves estrangerias das outras tabelas;
> A tabela 1 refletirá o cadastro de usuários do banco. Serão cadastrados apenas 5 usuários nesta tabela;
> Alguns atributos sugeridos para tabela 1 são: Nome, Idade, Sexo, CPF. Use mascaras como "***" nos dígitos que se referirem à dados sensíveis, mostrando apenas os últimos 2 números no caso de cpf; 
> A tabela 2 refletirá dados sobre o cartão dos usuários, como número e bandeira. Deixo ao seu critério quanto a forma de criação de ambos. Peço apenas para manter o mesmo padrão de mascara com "***", deixando apenas os 4 últimos números visíveis nesse caso;
> A tabela 3 mostrará as mensagens enviadas aos usuários e as datas. Aqui os atributos serão: ID, Data de envio do anúncio e Anúncio. Deixe todos os atributos vazios, pois iremos preencher em um código ETL ao longo do projeto.

[REGRAS DO PROMPT]
> Faça o prompt direcionado ao GPT-4 Code Interpreter para que este elabore as 'REGRAS DAS TABELAS' em um arquivo do excel, onde cada tabela será uma aba do arquivo. Porém, antes da criação, é necessário que o usuário que esteja interagindo com o GPT-4 autorize e valide o prompt e as ações;
> Após criar o prompt, exiba previamente o resultado das três tabelas e peça validação do resultado. Caso não esteja satisfatório, itere a ação até que esteja satisfeito com o resultado;
> A primeira validação será o prompt de criação de todas as demais ações até a anterior. Quero que crie o prompt para o GPT-4 que performe o comando de criação das etapas supracitadas. A validação será iterada até que esteja satisfeito. Quando estiver, essa última etapa não será mais necessária.
```
Este é um exemplo de prompt, porém a partir deste o GPT retornou:

```
Para criar as tabelas no contexto de um banco, precisamos de sua autorização. Você autoriza a criação destas tabelas conforme descrito?

Se sim, prosseguiremos da seguinte forma:

Criaremos a tabela de cadastro de usuários com os seguintes atributos:

ID
Nome
Idade
Sexo
CPF (formatado como ..***-XX)
Criaremos a tabela de dados do cartão com os seguintes atributos:

ID (referente ao usuário)
Número do cartão (com mascaramento ** ** **** XXXX)
Bandeira
Nota: Alguns usuários podem ter mais de um cartão associado.

Criaremos a tabela de mensagens enviadas com os seguintes atributos:

ID (inicialmente nulo, referente ao usuário)
Data de envio do anúncio (inicialmente vazia)
Anúncio (inicialmente vazio)
Após a criação, exibiremos as tabelas para sua validação. Caso esteja tudo correto, salvaremos em um arquivo Excel, onde cada tabela será uma aba distinta. Caso contrário, ajustaremos conforme suas instruções.

Você autoriza a prosseguir?
```

Após a validação, o Code Interpreter é ativado e cria o arquivo excel com os dados do comando. O resultado pode ser encontrado no link abaixo:

[Base de dados Excel - GPT-4](https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fraw.githubusercontent.com%2FIsraelEvangelista%2FSantander_Bootcamp_2023%2Fmain%2FProjeto%2520ETL%2520com%2520Python%2520com%2520IA%2520Generativa%2FBD_ETL_Santander2023.xlsx&wdOrigin=BROWSELINK)

**Conclusão**

Certo, vamos colocar as cartas na mesa. O GPT e outras IAs Generativas são, simplesmente, uma revolução quando se trata de criar bancos de dados para estudos e pesquisas. Lembra daqueles dias em que passávamos horas quebrando a cabeça para compilar informações? Com essa tecnologia, é como ter um assistente 24/7 pronto para gerar e organizar dados pra gente.

Mas, não para por aí. Está sem inspiração? Essas IAs dão um empurrãozinho na criatividade e podem abrir portas para insights que talvez nem tivéssemos considerado. Elas são como aquela xícara de café que dá o gás na hora da brainstorming.

Agora, é claro que nem tudo são flores, e a gente precisa usar essas ferramentas com discernimento. Mas, no fim do dia, a capacidade de agilizar processos, criar novas ideias e potencializar estudos com o auxílio do GPT e seus "amigos" é uma baita mão na roda.

## Metodologia de Extração

Com o arquivo Excel hospedado no Github, iniciamos o script ETL no COLAB. A primeira etapa do processo começa com a extração. Iremos portanto, carregar os dados de nossa base para o COLAB. Segue abaixo etapa do código:

```
import pandas as pd

# Base de dados gerado pelo prompt GPT-4, importadas de arquivo excel via Github
url = "https://raw.githubusercontent.com/IsraelEvangelista/Santander_Bootcamp_2023/main/Projeto%20ETL%20com%20Python%20com%20IA%20Generativa/BD_ETL_Santander2023.xlsx"
df1 = pd.read_excel(url, sheet_name='Cadastro de Usuários')
df2 = pd.read_excel(url, sheet_name='Dados do Cartão')
df3 = pd.read_excel(url, sheet_name='Mensagens Enviadas')
```

Em nosso prompt, criamos três tabelas: 
- Cadastro de Usuários
- Dados do Cartão
- Mensagens Enviadas

Todas elas estão unidas por uma chave primária "ID". No comando acima, nomeamos cada tabela com um dataframe diferente. df1, df2 e df3, respectivamente.

## Metodologia de Transformação

Como é de praxe em uma análise ETL, usamos o comando _dtypes_ para analisar os formatos de nossos atributos.

```
print(f"Cadastro de Usuários")
print(df1.dtypes)
print("\n")
print(f"Dados do Cartão")
print(df2.dtypes)
print("\n")
print(f"Mensagens Enviadas")
print(df3.dtypes)
```
Saída:
```
Cadastro de Usuários
ID        int64
Nome     object
Idade     int64
Sexo     object
CPF      object
dtype: object


Dados do Cartão
ID                   int64
Número do cartão    object
Bandeira            object
dtype: object


Mensagens Enviadas
ID                          object
Data de envio do anúncio    object
Anúncio                     object
dtype: object
```
Na saída, verificamos que em Mensagens Enviadas (df3), o ID não está em _int64_ como os demais. Para isso aplicamos a formatação. Assim como o formato de "Data de envio do anúncio" não está em _datetime_
```
df3['ID'] = df3['ID'].astype('int64')
df3["Data de envio do anúncio"] = pd.to_datetime(df3["Data de envio do anúncio"])
```
Para uma melhor visualização dos nossos dados, vamos usar o comando _merge_, similar ao _left join_ de bancos de dados relacionais, em nossos três dataframes.

```
df = pd.merge(df1, df2, on="ID", how="outer")
df = pd.merge(df, df3, on="ID", how="outer")
```
Com isso, temos uma única tabela com nossos dados agrupados:

Saída:

```
| ID | Nome             | Idade | Sexo      | CPF            | Número do cartão    | Bandeira  | Data de envio do anúncio | Anúncio |
|----|------------------|-------|-----------|----------------|---------------------|-----------|--------------------------|---------|
| 1  | Ana Silva        | 25    | Feminino  | ***.***.***-37 | **** **** **** 3307 | Visa      | NaT                      | NaN     |
| 1  | Ana Silva        | 25    | Feminino  | ***.***.***-37 | **** **** **** 5983 | Visa      | NaT                      | NaN     |
| 2  | João Costa       | 30    | Masculino | ***.***.***-85 | **** **** **** 3151 | Elo       | NaT                      | NaN     |
| 3  | Maria Santos     | 27    | Feminino  | ***.***.***-34 | **** **** **** 5209 | MasterCard| NaT                      | NaN     |
| 3  | Maria Santos     | 27    | Feminino  | ***.***.***-34 | **** **** **** 2733 | Visa      | NaT                      | NaN     |
| 4  | Lucas Ferreira   | 29    | Masculino | ***.***.***-75 | **** **** **** 5916 | Amex      | NaT                      | NaN     |
| 5  | Fernanda Oliveira| 31    | Feminino  | ***.***.***-14 | **** **** **** 5642 | Elo       | NaT                      | NaN     |
```

Para a etapa de gerar os anúncios, optei por usar um outro método diferente do proposto pelo projeto. O motivo, deve-se ao fato de já ter usado a API da OpenAI em outro momento, sendo impossível usá-la de forma gratuíta mais uma vez. 

A lógica da IA Generativa para criar mensagens, consiste em agrupar a oração principal de busca com outras dentro do contexto do que foi solicitado. A acurácia com que a IA acerta essas integrações vai depender do nível de treino que ela passou. Usando essa mesma ideia, mas de forma mais simplificada, criei duas listas onde elas serão integradas (uma por chave e a outra por chamada de ação) ao nome do usuário para formar a frase. No caso deste projeto, a ideia era formar anúncios unindo o nome do usuário às duas frases para formar o anúncio completo. Segue o exemplo do código abaixo:

```
import random
import datetime

# Ampliando a lista de frases-chave
frases_base = [
    "{Nome}, conquiste seus sonhos",
    "{Nome}, invista no futuro",
    "{Nome}, dê o primeiro passo",
    "{Nome}, sua chance de brilhar",
    "Oportunidade única para {Nome},",
    "{Nome}, transforme suas finanças",
    "Seu futuro começa agora, {Nome},",
    "{Nome}, faça o dinheiro trabalhar para você",
    "A jornada rumo à prosperidade espera por {Nome},",
    "{Nome}, realize mais, invista conosco"
]

# Ampliando a lista de chamadas à ação (CTA)
ctas = [
    " com nosso título de capitalização!",
    "! Adquira já e sinta a diferença!",
    " com as melhores taxas do mercado!",
    ". Venha conferir nossos planos!",
    "! Não perca esta chance!",
    ". Aproveite enquanto é tempo!",
    "! Junte-se aos vencedores!",
    ". Uma decisão inteligente!",
    "! Seu futuro financeiro aguarda!",
    ". Estabilidade e confiança aqui!"
]

# Função adaptada para gerar anúncio personalizado usando um registro de usuário
def gerar_anuncio_personalizado(user):
    frase = random.choice(frases_base).format(Nome=user['Nome']) + random.choice(ctas)
    while len(frase) > 150:  # Garantir que o anúncio tenha no máximo 150 caracteres
        frase = random.choice(frases_base).format(Nome=user['Nome']) + random.choice(ctas)
    return frase

# Iterando sobre 10 registros aleatórios de df1 e gerando anúncios personalizados
amostra = df1.sample(n=min(10, len(df1)))

for _, user in amostra.iterrows():
    anuncio = gerar_anuncio_personalizado(user)
    data_envio = datetime.datetime.now().strftime('%Y-%m-%d %H:%M:%S')
    novo_registro = {"ID": user["ID"], "Data de envio do anúncio": data_envio, "Anúncio": anuncio}
    df3 = df3.append(novo_registro, ignore_index=True)

# Mostrando os novos registros em df3
df3.tail(len(amostra))
```
Vamos explorar esse código:

**Importação**
Foram importadas as bibliotecas _random_ e _datetime_, usadas respectivamente para seleção de itens aleatórios de uma lista e usado para trabalhar com datas e horas.

**Listas para formar o Anúncio**
Foram criadas duas listas, uma de base e uma CTA (Chamadas à Ação). A lista base carrega também a chave {Nome} que será substituído pelo nome do usuário ao iterirar com o ID respectivo. Essa base será integrada à uma lista CTA aleatoriamente para formar um anúncio.

**Limite de 150 Caracteres**
while len(frase) > 150: Garante que a frase final tenha no máximo 150 caracteres, caso contrário, ela repete o processo.

**Selecionando uma amostra de usuários**
Aqui, uma amostra de no máximo 10 registros é retirada do dataframe df1 usando df1.sample(n=min(10, len(df1))). O min(10, len(df1)) garante que, se df1 tiver menos de 10 registros, ele simplesmente pegará todos eles.

**Iteração sobre a amostra**
Para cada usuário na amostra, a função _gerar_anuncio_personalizado_ é chamada para criar um anúncio. As datas e horas atuais são registradas e armazenadas em "Data de envio do anúncio".

## Metodologia de Carregamento (Load)

Com todas as alterações efetuadas, é hora da última etapa do processo ETL. O carregamento (Load). Aqui, serão refletidas todas as modificações em nosso arquivo base. Para tal, é gerado um novo arquivo excel com todas as alterações persistidas.

```
with pd.ExcelWriter('BD_ETL_Santander2023_modificado.xlsx', engine='openpyxl') as writer:
    df1.to_excel(writer, sheet_name='Cadastro de Usuários', index=False)
    df2.to_excel(writer, sheet_name='Dados do Cartão', index=False)
    df3.to_excel(writer, sheet_name='Mensagens Enviadas', index=False)

from google.colab import files
files.download('BD_ETL_Santander2023_modificado.xlsx')
```

Com o arquivo gerado, basta atualizarmos a base original hospedada no Github.
