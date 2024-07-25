const prompt = require('prompt-sync')();

const jogos = [];

const lerIndice = mensagem => parseInt(prompt(mensagem))

const nomeInvalido = nome => nome == ""

const indiceInvalido = indice => indice < 0 || indice >= jogos.length || isNaN(indice)


const listagem = () => jogos.forEach((jogo, i) => { 
    let sequencia
    if(jogo.sequencia != -1) {
        sequencia = jogos[jogo.sequencia].nome
    } else {
        sequencia = "Não possui sequência"
    }
    console.log(`${i + 1} - ${jogo.nome} - ${jogo.ano} - ${jogo.duracao} - ${jogo.preco} - ${jogo.estudio} - ${sequencia}`)
})

const modelo = () => {

    let jogo = {} // não posso adicionar atributos em algo indefinido

    while(true) {
        jogo.nome = prompt("Qual é o nome do jogo? ");
        if(nomeInvalido(jogo.nome)) {
            console.log("O nome não pode ser vazio");
        } else {
            break
        }
    }

    while(true) {
        jogo.ano = parseInt(prompt("Qual é o ano do jogo? "));
        if(jogo.ano < 1958 || jogo.ano > 2024 || isNaN(jogo.ano)) {
            console.log("O ano é inválido");
        } else {
            break
        }
    }

    while(true) {
        jogo.duracao = Number(prompt("Qual é o duração do jogo? ").replaceAll(",", "."));
        if(jogo.duracao <= 0 || isNaN(jogo.duracao)) {
            console.log("A duração é inválida");
        } else {
            break
        }
    }

    while(true) {
        jogo.preco = Number(prompt("Qual é o preço do jogo? ").replaceAll(",", "."));
        if(jogo.preco != 0 || isNaN(jogo.preco)) {
            console.log("O preço é inválido");
        } else {
            break
        }
    }

    while(true) {
        jogo.estudio = prompt("Qual é o estudio do jogo? ");
        if(nomeInvalido(jogo.estudio)) {
            console.log("O estudio não pode ser vazio");
        } else {
            break
        }
    }

    while(true) {

        if(jogos.length == 0) {
            jogo.sequencia = -1
            break
        }

        listagem()

        jogo.sequencia = lerIndice("Qual é a sequencia do jogo? Digite 0 caso não houver sequencia") - 1;

        // jogos.forEach((el, i) => {
        //     if(el.nome == jogo.sequencia) {
        //         jogo.sequencia = i
        //         return
        //     }
        // })

        if(jogo.sequencia != -1 && indiceInvalido(jogo.sequencia)) {
            console.log("A sequencia é invalida");
        } else {
            break
        }
    }

    return jogo
}
const criar = () => {

    const jogo = modelo()

    jogos.push(jogo)

    console.log("Jogo criado com sucesso")
}

const atualizar = () => {

    while(true) {

        if(jogos.length == 0) {
            console.log("Lista de jogos vazia")
            break
        }

        listagem()

        const indice = lerIndice("Qual é o indice do jogo que deseja atualizar? ") - 1

        if(indiceInvalido(indice)) {
            console.log("Indice inválido")
        } else {
            const jogo = modelo()
            jogos[indice] = jogo
           break
        }
    }

}

const remover = () => {

    while(true) {

        listagem()

        const indice = lerIndice("Qual é o indice do jogo que deseja remover? ") - 1

        if(indiceInvalido(indice)) {
            console.log("Indice inválido")
        } else {
            jogos.forEach(jogo => {
                if(jogo.sequencia == indice) {
                    jogo.sequencia = -1
                }
            })
            jogos.splice(indice, 1)
            console.log("Jogo removido com sucesso")
            break
        }
    }

}

module.exports = {
    criar,
    atualizar,
    remover,
    listagem
}