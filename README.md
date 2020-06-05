# Next Level Week #1

> Repositório usado para salvar projeto desenvolvido na NLW #1

## Usados

* Insomnia
* NodeJS
* ReactJS
* React Native
* Typescript


## Anotações

server.ts
```ts
import express from 'express';

const app = express();

app.use(express.json()); //Usado para o express entender o formato JSON do corpo da requisição

//Rota: Endereço completo da requisição
//Recurso: Qual entidade estamos acessando do sistema

//Request param: parâmetro que vem da própria rota e identifica um recurso
//Query param: parâmetros que vem da própria geralmente opcionais para filtros, paginação, etc
const users = [  
    "Guilherme",
    "Amariles",
    "Niara",
    "Amor"
]

app.get("/users", (request,response)=>{
    const search = String(request.query.search); //Forçado a ser String pra evitar vir um array

    const filteredUsers = search ? users.filter(user => user.includes(search)) : users;

    //Use return, pois impede do código prosseguir pra baixo do responde 
    return response.json(filteredUsers);
});

app.get("/users/:id", (request,response)=>{
    const id = Number(request.params.id); //Cast pra Number (2) porq vem como string ("2") 

    const user = users[id];

    return response.json(user);
});

app.post("/users", (request,response)=>{
    const data  = request.body; 

    console.log(data);

    const user = {
        name: data.name,
        email: data.email
    }

    return response.json(user);
});


app.listen(3333);
```
