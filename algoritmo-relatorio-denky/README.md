
# Relatorio do Algoritmo do denky

* <a href="https://github.com/Ashley-Lab/Ashley/blob/master/resources/boosters.py">Link do Algoritmo</a>

### Introdução

Aqui iremos "narrar" a maioria das coisas que acontece no algoritmo do bot feito em python usando a api do discord chamada Ashley, porem para entender 100% do que realmente acontece no algoritmo, recomendamos estudar primeiro a linguagem e depois ler esse relatorio.

De inicios vemos que é chamado 2 métodos  de random sendo eles radint e choice, agora qual a função dos 2? Só continuar lendo o código e iremos descobrir

Logo apos isso vemos que foi declarado uma classe com a palavra chave class e é passado como nome Booster. Depois que é declarado a classe é definido 6 métodos na classe, sendo eles: 

    * __init__ que recebe 2 parametros self e items_ e é chamado assim que a classe é construida, parecido com a declaração da palavra chave constructor nas classes em javacript não?

    * reset_counts 

    * create_box e como o nome já fala, tem a função dee criar a caixa.

    *buy_box que como o nome já fala terá a função de comprar caixas e recebe 2 parametros sendo eles bot e ctx

    * buy_items que recebe como parametro box_, ranking, e is_vip e terá como função comprar itens

    * buy_booster - parametros bot e ctx e terá como função comprar boosters

# Método __init__ 

Como eu não sou de python tive que fazer uma pequena colinha na documentação e descobri que esse método é chamado na construção da classe, igual em javascript então tudo que acontecer aqui nesse método será executado assim que a classe for instanciada:
    
    - É definido uma propriedade items que recebe o valor de items_ que terá como função representar os itens, e abaixo vemos que é declarado outras propriedades... sendo as que contem um valor inicial identico(None) ranking, is_vip, item_ e key_item

    - Agora é definido 3 propriedades no objeto da classe que terá como função represesentar a configarão das caixas

    - Logo apos isso tbm vemos que é definido  5 propriedades na classe que irá representar as chances de cada booster receber tal caixa.

    - Agora vemos que é definido propriedades que servirão como contadores de itens

    - É definido outra propriedade que será o contador de itens por caixa

    - Definido propriedades que irão representar o limite de cada item que pode ser obtido em uma caixa

# Método reset_counts

Esse método como o nome já fala terá como função resetar o contador e quando ele for chamado irá ser executado as seguintes tarefas:
    - A propriedade box agora vale seu valor inicial que foi mostrado no método __init__
    - As propriedades box_count, secret, ur, sr, r, i e c terá seus valores alterados para 0
    - Fim da função.

# Método create_box:

Novamente irei dizer, como o nome já fala esse método será responsável por criar caixas (create = criar, box = caixa) e quando o método é chamado ele fará:
    - Chamar o método reset_counts para resetar os contadores

    - rarity passa a valer o valor que é retornado do método chamado choice que recebe como parametro as keys do objeto da propriedade rarity da classe
    
    - size passa a valer  a propriedade de rarity(propriedade de classe) cujo nome seja o da variavel de escopo rarity

    - Então a propriedaded rarity que se encontra na propriedade status de box passa a valer o valor que está armazenado na variavel rarity e o mesmo acontece com a propriedade size porem o valor novo passa a ser o da variavel size

    - Agora é modificado o valor da propriedade items de box cujo valor passa a ser o do método dict chamado(valor de retorno)
    
    - Agora é feito um repetidor com a seguinte condição enquanto o valor da propriedade box_count for menor que o valor da propriedade size, faça isso...

        - No repetidor a primeira coisa que vemos que é declarado uma variavel com o nome item que recebe uma key aleatoria da propriedade items

        - Agora é feito uma condição(if & elif) onde fala que se a propriedade da propriedade(da classe) items cujo nome seja o valor da variavel item(que seria um array) e na posição 3 do array for igual a 5 irá ser feito:

            - Agora é feito outra condição onde se o valor da propriedade secret(classe) for menor que o valor da propriedade l_secret(classe):
                - Agora se o valor da variavel item não estiver na propriedade box(classe):
                    - propriedade items de box(classe) passa a valer tal valor
                    - propriedade status da propriedade status de box passa a receber seu valor + 1
            Agora foi aberto varios blocos com condições (elif) que foi basicamente isso aqui só que modificando com outros valores
# Método buy_box

De primeira vemos que esse método é responsável por comprar uma caixa e que nele será usado o banco de dados:
    - Vemos que é definido uma variavel que será responsavel por armazenar as informações do usuário registradas no banco de dados
    - É verificado se o dinheiro armazenado do usuário na db é maior que 2000 e se realmente for vai ser subtraido o valor de 2000 do dinheiro dele, mas caso não seja maior que 2000 é retornado um erro.
    - Agora é alterado o valor de data, e que eu acredito ser os dados atualizados no banco de dados
    - É declarado uma variavel com o nome update e ela recebe o valor da data e como eu pensei, é o valor atualizado da db
    - é declarado outra variavel onde dessa vez ela recebe o valor do método create_box da classe
    - É armazenado uma caixa no inventario nos valores armazenados na variavel update
    - Agora realmente é oficializado atualizando esses dados no banco de dados
    - É enviado uma resposta ao usuário e a mensagem "A BOX ENCONTRA-SE NA SUA CAIXA"

# Método buy_item

Agora nesse método vemos que ele será responsável por fazer a compra do item e terá que ser passado na chamada 3 parametros o box_, ranking e o is_vip e que finalmente é alterado os valores de algumas propriedades que estavam o valor None sendo elas ranking e is_vip:

    - O valor da propriedade(classe) ranking passa a valer o mesmo valor do parametro ranking passado na chamada da função e o mesmo vale para o is_vip

    - É feito uma sequencia de condições mas a ideia principal é "setar" o booster caso o ranking passado como parametro na chamada tenha um booster mas caso não tenha não é feito nada, ja que como sabemos o valor padrão ja é Choice

    - Agora é verificado se o valor do parametro is_vip é true, pois se for é "setado" o vip dele

    - É definido uma variavel com o nome chance que recebe um valor aleatorio de 1 a 100

    - Se o valor da variavel chance for igual a 100 o booster da pessoa passa a ser o secret

    - É definido uma variavel list_items que recebe um array e depois é feito um loop pra pecorrer cada elemento
    desse array.

    - É feito outro loop onde nesse é dado a condição para se repetir, caso True continue sendo True:
    No Loop é definido uma variavel com o nome result q recebe o valor retornado da função choice com o valor
    de list_items passado como parametro e uma condição pra verificar se a propriedade result que se encontra
    em uma das propriedades de box_ é maior que 0, se for é definido uma propriedade item na classe onde o valor
    é um valor aleatorio da propriedade items de box_

    - É retornado o valor da propriedade item_(prop da classe)

# Método buy_booster

É o método responsavel pelo ato de comprar um booster 
e deve ser passado como parametro o bot e o ctx e é
requisitado os valores armazenados do usuário armazenado
no parametro ctx e guardado na variavel data

    - É aberto 1 bloco catch e 1 bloco except onde no bloco try
    pe verificado se o valor da propriedade active no banco de 
    dados é true, para chegar nessa propriedade precisa passar
    pela propriedade box depois status e assim na active(tudo da variavel data)
    se for não faz nada, mas caso não seja true é retornado um erro
    na forma de mensagem para o usuário e caso tenha algum erro na
    hora de executar essas linhas é retornado um erro para o usuário
    onde fala "VOCÊ PRECISA COMPRAR UMA BOX PARA PODER COMPRAR UM
    BOOSTER"

    - Se a propriedade money for maior que 200(prop em data) é retirado
    o valor de 200 no saldo do usuário que comprou o booster,
    mas caso ele não tenha um valor abaixo de 200 é retornado um erro

    - Agora é executado as linhas para "entregar" o booster onde na verdade
    se está atualizando no banco de dados colocando uma booster nos dados
    registrados dele na db.
