# NODOX - APIs


## AUTH:

Endpoint: 
```javascript
`https://nodox.nodoxapp.com/api/auth`
```

Método: 
```javascript
`POST`
```

Body: 
```javascript
body = {
    email: 'usuario@tuemail.com',
    password: 'TuPassword'
}
```

Ejemplo: 
```javascript
async function auth(){

    let data = [];

    let body = {
        email: 'usuario@tuemail.com',
        password: 'TuPassword'
    }        

    await fetch(`http://nodox-qa.nodoxapp.com/api/auth`, {
        method: "POST",
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(body)
    })        
    .then(async function(response) {
        data = await response.json();
        let tuHash = data.hash; // Token de autentificación
    })             
    .catch(function(err){
        return err;
    })        
    return data;        
}

```


## GET:

Endpoint: 
```javascript
`https://nodox.nodoxapp.com/api/`
```

Método: 
```javascript
`GET`
```

Parámetros aceptados: 

+ **data** *- STRING* : Nombre de la tabla a la que se quiere acceder. Es el único parámetro obligatorio.
```javascript
data = 'usuarios' || 'audiencias' || 'encuestas' || 'respuestas' || 'productos' || ...
```

+ **creacion** *- STRING* : Trae datos creados en la fecha enviada. No compatible con "desde" o "hasta". 
```javascript
crecion = '2022-05-12'
```

+ **desde** *- STRING* : Trae datos desde la fecha enviada. No compatible con "creación".
```javascript
desde = '2022-05-01'
```

+ **hasta** *- STRING* : Trae datos hasta la fecha enviada. No compatible con "creación".
```javascript
hasta = '2022-05-31'
```

+ **limite** *- STRING* : Cantidad de datos solicitados. 
```javascript
limite = '5' // por default, devuelve 100
```

+ **inicio** *- STRING* : Para paginar.
```javascript
limite = '10'
```

+ **orden** *- STRING* : Órden de los datos. Se conforma por el nombre del campo y "ASC" para órden ascendente, o DESC para órden descendente. 
```javascript
'email=ASC' // ordena por email alfabéticamente de la A  a la Z 
'id=DESC' // ordena por número de ID de manera descendente
```

+ **todos** *- BOOLEAN* : Al enviar true, trae también los datos eliminados.  
```javascript
todos = true // por default está en false
```

Ejemplo básico: 
```javascript
async function getData(){
    let data = [];      

    let url = `https://nodox.nodoxapp.com/api`
    let param1 = `?data=productos`; // trae productos
    let urlFinal = `${url}${param1}`
    
    await fetch(`${urlFinal}`, {
        method: "GET",
        headers: {
            'Content-Type': 'application/json',
            'Token': `${TU_TOKEN}`
        }
    })        
    .then(async function(response) {
        data = await response.json();
        if(data){
            let productos = data; // productos
        }
    })             
    .catch(function(err){
        return err;
    })        
    return data;        
}    
```

Otro ejemplo con más parámetros: 
```javascript
async function getData(){
    let data = [];      
    
    let url = `https://nodox.nodoxapp.com/api`
    let param1 = `?data=productos`; // trae productos
    let param2 = `&desde=2022-01-01`; // fecha "desde"
    let param3 = `&hasta=2022-05-01`; // fecha "hasta"
    let param4 = `&id=ASC`; // ordena por ID -> ASC
    let param5 = `&limite=20`; // trae 20 productos
    let urlFinal = `${url}${param1}${param2}${param3}${param4}${param5}`

    await fetch(`${urlFinal}`, {
        method: "GET",
        headers: {
            'Content-Type': 'application/json',
            'Token': `${TU_TOKEN}`
        }
    })        
    .then(async function(response) {
        data = await response.json();
        if(data){
            let productos = data; // productos
        }
    })             
    .catch(function(err){
        return err;
    })        
    return data;        
}    
```
