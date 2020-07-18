### Este projeto usa como principal dependência o [cors-anywhere](https://github.com/Rob--W/cors-anywhere)

### As instruções abaixo considera que você saiba criar um servidor Ubuntu. [Veja o exemplo na Digital Ocean](https://www.digitalocean.com/docs/droplets/how-to/create/). Também não abordarei aqui as questões de segurança e performace. Depois de criado seu servidor faça o acesso ssh e siga os passos.


### Atualize a lista de repositórios 
```
sudo apt-get update && sudo apt-get upgrade
```

### Instale Node e o NPM utilize a última versão LTS. 
```
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

sudo apt-get install -y nodejs
```
### Faça o clone do projeto e instale as dependência
```
git clone https://github.com/izidorio/proxy-cors

cd proxy-cors && npm install
```
### Por padrão o node vai escutar a porta 8080 e aceitar requisição de qualquer IP. Caso precise alterar modifique o .env
```
nano .env

# Listen on a specific host via the HOST environment variable
HOST=0.0.0.0
# Listen on a specific port via the PORT environment variable
PORT=8080

```
### Instale o PM2 para monitorar a execução da aplicação
```
npm install pm2 -g
```

### Inicie a aplicação com o PM2
```
cd ~/proxy-cors
pm2 start server.js --name proxy-cors
```

### Garanta que ao reiniciar o servidor a aplicação seja startada
```
pm2 startup

pm2 save
```

### Exemplo de uso 
```
import axios from 'axios'
const api = axios.create({
    baseURL: 'http://<IP_SERVIDOR>:8080'
})

async function getUser() {
  try {
    const response = await api.get('https://google.com');
    console.log(response);
  } catch (error) {
    console.error(error);
  }
}

```

## License

Copyright (C) 2013 - 2016 Rob Wu <rob@robwu.nl>

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies
of the Software, and to permit persons to whom the Software is furnished to do
so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.