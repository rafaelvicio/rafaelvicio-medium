Promisses em JavaScript para Leigos

O seguinte artigo e uma tradução do 'JavaScript Promisses for dummies' da Jecelyn Yeen. Pode ser visto em https://scotch.io/tutorials/javascript-promises-for-dummies#toc-promises-in-es5-es62015-es7next

Promisses em JavaScript não são dificies. No entando, muitas pessoas acham um pouco dificil de ententar no início. Portanto, eu gostaria de escrever a maneira como eu entendo as Promisses, de uma maneira boba.

#Compreendendo Promisses

Promisses de forma curta:

"Imagine que você e uma criança. Sua mãe promete que vai lhe dar um telefone novo na próxima semana."

Você não sabe se você irá receber o telefone até a semana que vem. Sua mãe pode realmente comprar um telefone novo ou negar se ela não estiver feliz.

Isso é uma promessa(Promisse). Uma promessa possue 3 estados. Eles são:

1. Promessa pendente: Você não sabe se você recebe o telefone até a semana que vem.  
2. Promessa resolvida: Sua mãe realmente compra um telefone novo.
3. Promessa rejeitada: Você não ganha um novov telefone porque sua mãe não está feliz.

#Criando uma Promisse

Vamos criar isso em JavaScript

"// ES5
var maeFeliz = false;

var voceRecebeUmNovoTelefone = new Promisse(
    function (resolve, reject) {
        if(maeFeliz){
            var phone = {
                marca: 'iPhone',
                cor: 'black'
            };
            resolve(phone) // IHUL!
        } else {
            var problema = new Error('Mãe não esta feliz :(');
            reject(problema);
        }
    }
)
"

O código é bastante simples.

1. Nós temos um booleano 'maeFeliz', para definir se ma mãe está ou não feliz.
2. Nõs temos uma Promisse, 'voceRecebeUmNovoTelefone'. A promessa pode ser cumprida(Se sua mãe estiver feliz, ela compra um telefone novo) ou rejeitada (Se a mãe não estiver feliz, ela não compra um telefone novo).
3. Existe uma sintaxe padrão para definir uma Promisse. consulte a documentação do MDN, a sintaxe é a seguinte:

"new Promise(function (resolve, reject) { ... } );"

4. O que você precisa lembrar e, se o resultado for um sucesso, chama 'resolve()', se o resultado falhar, chama 'reject()'. No nosso exemplo, se a mãe estiver feliz, elá compra um telefone novo. Portanto, chamamos a função 'resolve()' pasando o 'telefone'. Se a mãe não estiver feliz, nós chamamos a função 'reject()' passando o problema.

# Utilizando uma Promisse
Agora que temos uma promisse, vamos utilizar-la.

// ES5

// Chamando sua promisse

var PerguntandoParaMae = function() {
    voceRecebeUmNovoTelefone
        .then(function (sucesso){
            // Você recebe um novo telefone
            console.log(sucesso);
            // Imprime { marca: 'iPhone', cor: 'black' }
        })
        .catch(function(error){
            // Ops, a mãe não está feliz
            console.log(error.message);
        });
};

PerguntandoParaMae();

1. Nós temos a função chamada 'PerguntandoParaMae()'. NEsta função, vamos consumir a promisse 'voceRecebeUmNovoTelefone'.
2. Queremos realizar alguma ação uma vez que a promessa é resolvida ou rejeitada, usamos '.then' e '.catch' para tratar essas ações.
3. No nosso exemplo, temos a função 'function (sucesso)' no '.then'. Mas qual é o valor do 'sucesso'? O 'sucesso' é exatamente o valor que voce passou em sua solução 'resolve(phone)'.
4. Temos a função 'function(error)' em '.catch'. Mas qual o valor de 'error'? O valor é exatamente o que foi passado na nossa Promisse em 'reject()'. Portante, será o motivo do rejeição.

Vamos executar o exemplo para ver o resultado.

https://jsbin.com/nifocu/1/edit?js,console

# Encadeando Promisses

