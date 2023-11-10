# regexp

https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Guide/Regular_Expressions
Criador de expressÃµes regulares -->> https://regex101.com/

    ExpressÃµes Regulares
ExpressÃµes regulares sÃ£o padrÃµes utilizados para selecionar combinaÃ§Ãµes de caracteres em uma string. Em JavaScript, expressÃµes regulares tambÃ©m sÃ£o objetos. Elas podem ser utilizadas com os mÃ©todos exec (en-US) e test (en-US) do objeto RegExp (en-US), e com os mÃ©todos match (en-US), replace (en-US),search (en-US), e split (en-US) do objeto String. Este capÃ­tulo descreve o uso de expressÃµes regulares em JavaScript.

Expressoes regulares servem procurar coisas especificar dentro de um arquivo, editar essas mesmas coisa, validar componentes, formularios, entre outros.
Um padrao para voce procurar coisas dentro de textos, e com as mesmas posso fazer oque eu precisar com elas

// g - global - Encontra todas as ocorrencias - FLAG - GLOBAL
// i - INSENSITIVE (Nao verifica por letras maiusculas e minusculas)
// Metodo .test ira procurar no texto se tem ou nao aquela expressao - retorna true ou false
// () Grupos
// | ou == /(joao|maria)/

FunÃ§Ãµes match replace search e split do Objeto String

    const regExp = /palavra/i;
    console.log(texto.match(regExp))
        Retorna um array contendo o texto em si, a palavra buscada,o index dela e o grupo

    const regExp = /palavra/gi;
    console.log(texto.match(regExp))
        Retorna Quantas Expressoes contem no texto;

    console.log(texto.replace(/palavra/gi,'palavra'))
        Ira trocar todas as palavras que tiver no texto por outra que eu escolher

    console.log(texto.replace(/(palavra|outraPalavra)/gi,'"$1"'))
        Ira colocar aspas duplas em todas as palavras que tiver no texto
        // $1 Representa oque esta dentro dos parenteses

    console.log(texto.replace(/(joao|mar ia)/gi, function(input) {
        return input.toUpperCase() }))
        Transforma todas palavras 'joao' e 'maria' para Uppercase

    console.log(texto.replace(/(joao|maria)/gi, function(input) {
        return '#########' + input.toUpperCase() + '#########' }))
        Transforma todas palavras 'joao' e 'maria' >> ######### joao #########

Quantificadores * + ?
    + - Obrigatorio - Quantifica 1 ou mais vezes    {0,}
    * - Opicional - 1 ou N vezes    {1,}
    ? - Opicional -  0 ou 1 vez    {0,1}
    {n,m} - Quantidade de vezes Minimo e Maximo

    const regExp = /Jo+Ã£o/gi
    console.log(texto.match(regExp))
        Retorna todos os joao que tenham 1 ou mais letras 'o' no texto
        Caso tenhamos um 'joooaooooooo' ia retorna 'joooao'

    const arquivos = [
        'AtenÃ§Ã£o.jpg',
        'FOTO.jpeg',
        'Meu gatinho.jpg',
        'Meu gatinho.JPG',
        'Meu gatinho.JPEG',
        'Meu gatinho.JPeeEEEEeeeeeeeeeeeeeeeeeeeeeeeeEEEEEEEEEEG',
        'Marido.png',
        'lista de compras.txt', ];
    for(const arquivo of arquivos){
        console.log(arquivo)    }
            Retorna todos os itens do array

// Barra invertida '\' Usado para caractere de escape
    const regExp2 = /\./gi
    console.log(arquivos.match(regExp2))
        Retorna todos os pontos que tem no arquivo\

    const regExp2 = /\.jpg/gi
    console.log(arquivos.match(regExp2))
        Retorna todos os .jpg que encontrar, nao encontre retorna o indice como Nulo

    const regExp2 = /\.jpg/gi
    console.log(arquivos.match(regExp2))
        Retorna todos os .jpg que encontrar, nao encontre retorna o indice como Nulo

    const regExp2 = /\.jpe?g/gi
    console.log(arquivos.match(regExp2))
        Retorna todos os jpg e jpeg, o indicador '?' significa que por ter ou nao ter o 'e'

    const regExp2 = /\.jpe?g/gi
    const valido = arquivo.match(regExp2)
    if(!valido) continue
    console.log(arquivos.match(regExp2))
        Retorna todos os jpg e jpeg, e os nulos nao retornam

Greedy e non-Greedy (lazy) dos Quantificadores
    Podemos pegar todas os elementos html de uma pagina com o seguinte codigo
        const exemplo = '<p> Ola Mundo </p> <p> Ola Mundo Denovo </p>'
        const expReg = /<.+>.+<\/.+>/gi
        console.log(exemplo.match(expReg))
            Retorna '<p> Ola Mundo </p> <p> Ola Mundo Denovo </p>' - Greedy

        const expReg = /<.+?>.+?<\/.+?>/gi
        console.log(exemplo.match(expReg))
            Retorna '<p> Ola Mundo </p>' e '<p> Ola Mundo Denovo </p>' - Non-Greedy
            Retorna separadamente ou seja, retorna um array com 2 indices

Conjuntos e Ranges
    Conjunto >>> Qualquer coisa que esta dentro de colchetes serao um Conjunto
    Range >>> Entre colchetes [deAlgumaCoisa - ateOutraCoisa] Ex: [0-1]

    const alfabeto = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ abcdefghijklmnopqrstuvwxyz Â®Â¡ 0123456789 Â¡';
    console.log(alfabeto.match(/[abc]/g))
        Retorna um array com 3 elementos >>> 'a' 'b' 'c'

    console.log(alfabeto.match(/[abc]+/g))
        Retorna um array >>> 'abc'

    console.log(alfabeto.match(/[abc123]+/g))
        Retorna um array com 2 elementos >>> 'abc' '123'

    console.log(alfabeto.match(/[^abc123]/g))
        Retorna um array com tudo menos oque esta dentro dos colchetes, cada elemento com 1 index

    console.log(alfabeto.match(/[^abc123]+/g))
        Retorna um array com tudo menos oque esta dentro dos colchetes em uma unica string

    console.log(alfabeto.match(/[0-9]/g))
        Retorna um array com todos os numeros separados dentro array

    console.log(alfabeto.match(/[0-9]+/g))
        Retorna um array com todos os numeros juntos em uma unica string
            Caso eu tivese (012345 6789) Separando por espaÃ§o, Ele retornaria um array e 2 index

    console.log(alfabeto.match(/[a-z]/g))
        Retorna um array com todos as letras separados dentro array

    console.log(alfabeto.match(/[a-z]+/g))
        Retorna um array com todos as letras juntas dentro array

    console.log(alfabeto.match(/[A-Z]/g))
        Retorna um array com todos as letras separadas dentro array

    console.log(alfabeto.match(/[A-Z]+/g))
        Retorna um array com todos as letras juntas dentro array

    console.log(alfabeto.match(/[a-z0-9A-Z]/g))
        Retorna um array com todos as letras e todos os numeros tudo separado dentro do array

    console.log(alfabeto.match(/[a-z0-9A-Z]/g))
        Retorna um array com todos as letras juntas e todos os numeros juntos dentro do array

    console.log(alfabeto.match(/[^a-z0-9A-Z]/g))
        Retorna tudo menos de a-z A-Z e 0-9

    console.log(alfabeto.match(/\w+/g))
        Retorna tudo de a-z, A-Z e 0-9

    console.log(alfabeto.match(/\W+/g))
        Retorna tudo menos de a-z, A-Z e 0-9

    console.log(alfabeto.match(/\d+/g))
        Retorna tudo de 0-9

    console.log(alfabeto.match(/\D+/g))
        Retorna tudo menos de  0-9

    console.log(alfabeto.match(/\s/g))
        Retorna quantos espaÃ§os tem no texto

    console.log(alfabeto.match(/\s/g))
        Retorna tudo menos os espaÃ§os

Atividades CPF e iP
    const cpfs = "123.456.789-12 - 789.456.123-56 - 456.123.789-78";
    console.log(cpfs.match(/(\d{3}\.){2}\d{3}\-\d{2}/g));

    Para IPS
        /((25[0-5]|2[0-4]\d|1\d{2}|[1-9]\d|\d)(\.)){3}(25[0-5]|2[0-4]\d|1\d{2}|[1-9]\d|\d)/g

ComeÃ§a com e termina com:
    [^] o circunflexo dentro de colchetes '[^]' esta sendo lido como negaÃ§Ã£o
     ^  no inicio da expressao Significa 'comeÃ§a com'
     $  Diz 'termina com'
     m  multiline > flag > Muda o comportamento do ^ e $ > Ira checar Linha por linha inves da string inteira como um todo

     console.log(cpfs.match(/^(\d{3}\.){2}\d{3}\-\d{2}$/g));
     console.log(cpfs.match(/^(\d{3}\.){2}\d{3}\-\d{2}$/gm));

Retrovisores
    // $1 $2 $3 <- Retrovisores \1 \2 \3

    Caso tenha um grupo mas nao queira deixar ele como Retrovisor, colocaremos um '?:' depois da abertura dos parenteses -> '(?:\d)'

    Posso utilizar um grupo novamente funcionando similarmente a uma variavel, utilizando '\' e o numero do grupo -> '\2', Estaria pegando similarmente ao que ja foi pego da primeira vez

    console.log(text.match(/<(\w+)[\s\S]*?>[\s\S]*?<\/\1>/g))

Lookaround

    const lookahead = `
    ONLINE  192.168.0.1 ABCDEF inactive
    OFFLINE  192.168.0.2 ABCDEF active
    ONLINE  192.168.0.3 ABCDEF active
    ONLINE  192.168.0.4 ABCDEF active
    OFFLINE  192.168.0.5 ABCDEF active
    OFFLINE  192.168.0.6 ABCDEF inactive
    `;

// Positive lookahead (Frases que tem active)
// Retorna tudo menos a palavra que eu descever no '()' junto do '?=' ->  '(?=)'
    console.log(lookahead.match(/.+(?=[^in]active)/gim));

// Positive lookahead (Frases que tem inactive)
// Retorna tudo menos a palavra que eu descever no '()' junto do '?=' ->  '(?=)'
    console.log(lookahead.match(/.+(?=inactive)/gim));

// Negative lookahead (Frases que tem inactive)
// Semelhante a Positive lookahead porem ele retorna somente as frases que nao tiverem
// a expressao que pasar-mos no parenteses junto do '?!'
    console.log(lookahead.match(/^(?!.+[^in]active).+$/gim));

// Negative lookahead (Frases que tem active)
// Semelhante a Positive lookahead porem ele retorna somente as frases que nao tiverem
// a expressao que pasar-mos no parenteses junto do '?!'
    console.log(lookahead.match(/^(?!.+inactive).+$/gim));

// Positive lookbehind (Frases que comeÃ§am com ONLINE)
// Retorna as frases que tiverem a palavra passada dentro do parametro '(?<=)' porem sem esta palavra
console.log(lookahead.match(/(?<=ONLINE\s+)\S.*/gim));

// Negative lookbehind (Frases que nao comeÃ§am com ONLINE)
// Retorna a frase toda
console.log(lookahead.match(/^.+(?<!ONLINE.+)$/gim));

----------------------- FIM -----------------------
Exemplos:

// Encontra todas as palavras
const palavrasRegEx = /([\wÃ€-Ãº]+)/g

// NÃ£o nÃºmeros
const naoNumerosRegEx = /\D/g

// Valida IP
const ipRegExp = /((25[0-5]|2[0-4][0-9]|1\d{2}|[1-9]\d|\d)(\.)){3}(25[0-5]|2[0-4][0-9]|1\d{2}|[1-9]\d|\d)/g;

// Valida CPF
const cpfRegExp = /(?:\d{3}\.){2}\d{3}-\d{2}/g

// Valida telefones
const validaTelefone = /^(\(\d{2}\)\s*)?(9\s*)?(\d{4})-(\d{4})$/g

// Validar senhas fortes
const validaSenhasFortes = /^(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[!@#$%\]\)]).{8,}$/g

// ##################################
// # Validar e-mails (use a Ãºltima) #
// ##################################

// [^\s]+@[^\s]+\.[^\s]+(\w+)* (Hiper Permissiva)

// Essa expressÃ£o Ã© bem permissiva, menos que a anterior,
// Mas ainda detecta bastante e-mails invÃ¡lidos
// [^\s\.]+\.?[^\s\.]+@[^\s]+\.[^\s]+\w+

// Em meus testes a regexp que obteve melhor resultado
// (acertando mais vÃ¡lidos e invÃ¡lidos)
// Foi a da linha a seguir:
// /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/

const validaEmail = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
