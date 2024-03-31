<h1>Tutorial de Instalação Flask e React</h1>

Instalar as ferramentas necessárias para o desenvolvimento de um software web em um sistema operacional Linux baseado em Debian (como Debian, Ubuntu ou Mint) envolve vários passos. Este tutorial detalhado abordará a instalação do Python e do Flask (um framework web Python), do Node.js e do React (uma biblioteca JavaScript para construção de interfaces de usuário), e do PostgreSQL em um container Docker.

<h3>Instale as dependências necessárias</h3>
Alguns pacotes são essenciais para o desenvolvimento de software e para as etapas seguintes deste tutorial. Instale-os com:

```bash
sudo apt install -y build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
xz-utils tk-dev libffi-dev liblzma-dev python-openssl git
```
<h2>Etapa 2: Instalando Python e Flask</h2>
1 - Instale o Python: O Ubuntu geralmente vem com o Python pré-instalado. Você pode verificar a versão do Python com python3 --version. Se necessário, instale o Python 3 com:

```bash
sudo apt install -y python3 python3-pip python3-venv
```

1.1 - Após instalar o Python crie as pastas dos seus projetos. Crie uma pasta para o projeto e dentro dela crie duas pastas: backend e frontend.

1.2 - Abra a pasta de backend no Vscode ou na sua IDE de preferência e ative o console para digitar os comandos necessários.

2 - Crie um ambiente virtual: Para manter as dependências do projeto isoladas, é uma boa prática usar um ambiente virtual. Crie um para o seu projeto Flask:

```bash
python -m venv myprojectenv
source myprojectenv/bin/activate
```

3 - Instale o Flask: Com o ambiente virtual ativado, instale o Flask usando o pip:

```bash
pip install Flask
```

<h2>Etapa 3: Instalando Node.js e React</h2>
1 - Instale o Node.js: Node.js é necessário para o desenvolvimento com React. Você pode instalar a versão mais recente do Node.js usando o NVM (Node Version Manager), o que permite gerenciar múltiplas versões do Node.js:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
nvm install --lts
```

<h2>Etapa 4: Configurando o Docker e PostgreSQL</h2>
1 - Instale o Docker: Primeiro, instale o Docker para poder rodar containers:

```bash
sudo apt install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
```
2 - Execute o PostgreSQL em um container Docker: Você pode executar uma instância do PostgreSQL dentro de um container Docker:

```bash
docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d -p 5432:5432 postgres
```

"--name" define o nome do seu container.
"-e" configura variáveis de ambiente, neste caso, a senha do superusuário do PostgreSQL.
"-d" executa o container em segundo plano.
"-p" mapeia a porta 5432 do container para a porta 5432 do host.

<h2>Etapa 5: Criando e Iniciando um Projeto Flask</h2>
Após ter instalado o Python e o Flask, conforme explicado anteriormente, você está pronto para criar e iniciar um projeto Flask.

1 - Volte para seu diretório de backend com o flask:

2 - Ative o ambiente virtual que você criou anteriormente (se você seguiu o tutorial desde o início, caso contrário, crie um novo ambiente virtual como explicado antes):

```bash
source ../myprojectenv/bin/activate
```

3 - Crie um arquivo chamado app.py. Este será o arquivo principal da sua aplicação Flask:

```bash
touch app.py
```

4 - Abra este arquivo em um editor de texto de sua preferência e adicione o seguinte código:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Olá, Mundo!'

if __name__ == '__main__':
    app.run(debug=True)
```
Este código cria uma aplicação Flask simples com uma rota que retorna "Olá, Mundo!".

5 - Execute o aplicativo Flask. Certifique-se de que seu ambiente virtual ainda esteja ativado, e execute o seguinte comando no terminal:

```bash
python app.py
```

Você verá que o servidor Flask está rodando e acessível em http://127.0.0.1:5000/ Ao acessar este endereço em um navegador, você verá a mensagem "Olá, Mundo!".

<h2>Etapa 6: Criando e Iniciando um Projeto React</h2>
Após instalar o Node.js e o NPM, você está pronto para criar e iniciar um projeto React.

1 - Abra sua pasta de frontend no VsCode e ative o terminal para digitar os seguintes comandos.

1.2 - Crie um novo aplicativo React usando o Create React App, uma ferramenta oficialmente suportada que cria um front-end React com uma boa configuração padrão. Substitua meu-app-react pelo nome que desejar para seu aplicativo:

```bash
npx create-react-app meu-app-react
```
Este comando cria um novo diretório chamado meu-app-react (ou o nome que você escolheu) com todos os arquivos necessários para começar a desenvolver um aplicativo React.

2 - Entre no diretório do seu aplicativo:

```bash
cd meu-app-react
```

3 - Inicie o servidor de desenvolvimento do React com o seguinte comando:

```bash
npm start
```

Esse comando inicia um servidor de desenvolvimento e abre uma janela do navegador mostrando seu aplicativo React. Por padrão, o aplicativo React está acessível em http://localhost:3000/

Você verá uma página inicial do React, indicando que o aplicativo foi criado e iniciado com sucesso.

<h2>Etapa 7: Criando uma Rota no Back-End com Flask</h2>

1 - No diretório do seu projeto Flask, abra o arquivo que contém as definições de rota, neste caso será o arquivo app.py

2 - Adicione o seguinte código para criar uma nova rota:

```python
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/teste', methods=['GET'])
def teste():
    return jsonify(message="Rota executou com sucesso!"), 200

if __name__ == '__main__':
    app.run(debug=True)
```

3 - Salve o arquivo e reinicie seu servidor Flask para que as mudanças tenham efeito. Se o debug estiver ativado, ele deve recarregar automaticamente.

Agora, qualquer requisição GET para /teste retornará um JSON com a mensagem "Rota executou com sucesso!".

<h2>Etapa 8: Configurando o Front-End com React</h2>

LEMBRANDO: Ambas as aplicações devem estar rodando juntas, então será necessário ter 2 VsCode aberto com o backend e o frontend rodando.
Essa abordagem pode ser mais complicada mas é a mais próxima do mercado de trabalho atualmente.

1 - No diretório do seu projeto React, você vai criar uma interface para interagir com a rota Flask. 
Primeiro, instale o Axios, uma biblioteca que facilita as requisições HTTP, com o seguinte comando:

```bash
npm install axios
```

2 - No seu componente React, você vai adicionar um botão que, ao ser clicado, fará a requisição para a rota /teste e exibirá a mensagem. Aqui está um exemplo básico de como fazer isso:

```jsx
import React, { useState } from 'react';
import axios from 'axios';

function App() {
    const [message, setMessage] = useState('');

    const getTestMessage = () => {
        axios.get('http://localhost:5000/teste')
            .then(response => {
                setMessage(response.data.message);
            })
            .catch(error => {
                console.error('There was an error!', error);
            });
    };

    return (
        <div>
            <button onClick={getTestMessage}>Teste Rota</button>
            <p>{message}</p>
        </div>
    );
}

export default App;
```

3 - Inicie seu servidor React (se ainda não estiver rodando) com:

```bash
npm start
```

Agora, ao clicar no botão "Teste Rota" no seu aplicativo React, o front-end fará uma requisição para o back-end, o servidor Flask processará a rota /teste e retornará a mensagem "Rota executou com sucesso!", que será então exibida no front-end.

<h2>Etapa 9: Atualizar a Rota no Flask para Aceitar Parâmetros</h2>

1 - Vá para o arquivo do seu projeto Flask que contém as definições das rotas (geralmente app.py).
Adicione um novo parâmetro dinâmico à rota existente ou crie uma nova rota se desejar manter a funcionalidade anterior:

```python
# app.py

from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/teste/<int:num>', methods=['GET'])
def teste(num):
    # A variável 'num' será o número fornecido na URL
    return jsonify(message=f"Rota executou com sucesso recebendo o valor {num}!"), 200

if __name__ == '__main__':
    app.run(debug=True)
```

2 - Certifique-se de reiniciar o servidor Flask para aplicar as mudanças.

3 - Agora no seu frontend React, você atualizará o componente para enviar o parâmetro na URL e tratar a resposta:
No arquivo do componente React (por exemplo, App.js), importe useState para manter o estado da mensagem.
Defina um estado para manter a resposta do servidor:

```javascript
// No topo do seu arquivo
import React, { useState } from 'react';
import axios from 'axios';

function App() {
    // Este estado guardará a resposta do servidor
    const [responseMessage, setResponseMessage] = useState('');
    
    // ...
}
```

4 - Crie uma função para fazer a requisição GET com o parâmetro:

```javascript
const getResponse = (param) => {
    axios.get(`http://localhost:5000/teste/${param}`)
        .then(response => {
            // Atualiza o estado com a resposta do servidor
            setResponseMessage(response.data.message);
        })
        .catch(error => {
            console.log(error);
        });
}
```

5 - Adicione um botão no JSX para chamar essa função passando o parâmetro desejado (neste caso, 10):

```javascript
// No método de renderização
return (
    <div>
        <button onClick={() => getResponse(10)}>Enviar Parâmetro 10</button>
        <p>{responseMessage}</p>
    </div>
);
```

6 - Certifique-se de que o React esteja rodando. Se você fez alterações, o servidor de desenvolvimento do React deve recarregar automaticamente.

Com essas mudanças, quando você clicar no botão "Enviar Parâmetro 10", o front-end fará uma requisição GET para a URL http://localhost:5000/teste/10, onde 10 é o parâmetro dinâmico. O servidor Flask processará a rota e retornará a mensagem "Rota executou com sucesso recebendo o valor 10!", que será então armazenada no estado responseMessage e exibida abaixo do botão no seu aplicativo React.

<h2>Etapa 10: Atualizando o Flask para Aceitar Parâmetros de Consulta</h2>

1 - Abra o arquivo do projeto Flask com as definições das rotas (geralmente app.py).
Modifique a função de rota para capturar os parâmetros de consulta usando o objeto request:

```python
from flask import Flask, jsonify, request

app = Flask(__name__)

@app.route('/teste', methods=['GET'])
def teste():
    # Captura os parâmetros de consulta 'valor' e 'quantidade'
    valor = request.args.get('valor', default=1, type=int)
    quantidade = request.args.get('quantidade', default=1, type=int)
    return jsonify(message=f"Rota executou com sucesso recebendo o valor {valor} e quantidade {quantidade}!"), 200

if __name__ == '__main__':
    app.run(debug=True)
```

2 - Aqui, request.args.get é usado para obter os parâmetros de consulta. Os argumentos default e type são usados para definir um valor padrão e o tipo esperado dos parâmetros, respectivamente.
Reinicie o servidor Flask para que as alterações entrem em vigor.

3 - Atualizando o Frontend React para Enviar Parâmetros de Consulta.
No front-end com React, atualize o componente para enviar os parâmetros de consulta na URL.
Defina uma nova função para enviar a requisição com os parâmetros de consulta:

```javascript
const getResponseWithQuery = () => {
    const queryParams = new URLSearchParams({ valor: 10, quantidade: 3 }).toString();
    axios.get(`http://localhost:5000/teste?${queryParams}`)
        .then(response => {
            // Atualiza o estado com a resposta do servidor
            setResponseMessage(response.data.message);
        })
        .catch(error => {
            console.log(error);
        });
}
```

4 - No exemplo acima, URLSearchParams é utilizado para criar uma string de parâmetros de consulta.

Adicione um botão no JSX que chama essa função quando clicado:

```jsx
return (
    <div>
        <button onClick={getResponseWithQuery}>Enviar Parâmetros de Consulta</button>
        <p>{responseMessage}</p>
    </div>
);
```

5 - Execute seu servidor React para ver as mudanças.

Agora, quando o botão "Enviar Parâmetros de Consulta" é clicado no aplicativo React, o front-end faz uma requisição GET para a URL http://localhost:5000/teste?valor=10&quantidade=3. O servidor Flask processa a requisição, capturando os parâmetros de consulta valor e quantidade, e retorna a mensagem "Rota executou com sucesso recebendo o valor 10 e quantidade 3!" que será exibida no front-end.

<h2>Etapa 11: Criando um Formulário no Front-End com React</h2>
Vamos criar um formulário no React que permita ao usuário entrar com diversos tipos de dados.

1 - No seu projeto React, abra o arquivo do componente onde você deseja adicionar o formulário (por exemplo, App.js) e adicione o seguinte estado inicial para armazenar os valores do formulário:

```jsx
import React, { useState } from 'react';

function App() {
    const [formData, setFormData] = useState({
        texto: '',
        inteiro: 0,
        booleano: false,
        opcaoSelect: '',
        opcaoRadio: ''
    });

```

2 - Adicione uma função para lidar com a mudança nos inputs e atualizar o estado do formulário:

```jsx
    const handleChange = (e) => {
        const { name, value, type, checked } = e.target;
        setFormData(prevFormData => ({
            ...prevFormData,
            [name]: type === 'checkbox' ? checked : value
        }));
    }
```

3 - Agora, vamos adicionar o JSX do formulário:

```jsx
    return (
        <div>
            <form>
                <input
                    name="texto"
                    type="text"
                    value={formData.texto}
                    onChange={handleChange}
                />
                <input
                    name="inteiro"
                    type="number"
                    value={formData.inteiro}
                    onChange={handleChange}
                />
                <label>
                    <input
                        name="booleano"
                        type="checkbox"
                        checked={formData.booleano}
                        onChange={handleChange}
                    />
                    Booleano
                </label>
                <select
                    name="opcaoSelect"
                    value={formData.opcaoSelect}
                    onChange={handleChange}
                >
                    <option value="">Selecione uma opção</option>
                    <option value="opcao1">Opção 1</option>
                    <option value="opcao2">Opção 2</option>
                </select>
                <div>
                    <label>
                        <input
                            type="radio"
                            name="opcaoRadio"
                            value="radio1"
                            checked={formData.opcaoRadio === "radio1"}
                            onChange={handleChange}
                        />
                        Radio 1
                    </label>
                    <label>
                        <input
                            type="radio"
                            name="opcaoRadio"
                            value="radio2"
                            checked={formData.opcaoRadio === "radio2"}
                            onChange={handleChange}
                        />
                        Radio 2
                    </label>
                </div>
                <button type="submit">Enviar</button>
            </form>
        </div>
    );
}

export default App;

```

<h2>Etapa 12: Enviando os Dados do Formulário para o Back-End</h2>

Para enviar os dados do formulário do front-end para o back-end, vamos utilizar o Axios no evento de submit do formulário.

1 - Adicione a biblioteca Axios ao seu projeto React (se ainda não o fez):

```bash
npm install axios
```

2 - Adicione a função handleSubmit ao seu componente para lidar com o envio do formulário:

```jsx
    const handleSubmit = (e) => {
        e.preventDefault();
        axios.post('http://localhost:5000/formulario', formData)
            .then(response => {
                console.log(response.data);
            })
            .catch(error => {
                console.error('There was an error!', error);
            });
    }
```

3 - Modifique a tag <form> para incluir o handleSubmit:

```jsx
<form onSubmit={handleSubmit}>
```

<h2>Etapa 13: Configurando o Back-End com Flask para Receber os Dados do Formulário</h2>
No lado do servidor Flask, você vai configurar uma rota para receber os dados do formulário e retornar uma resposta.

1 - Abra o arquivo app.py no seu projeto Flask e importe request do Flask:

```python
from flask import Flask, request, jsonify
```

2 - Adicione a rota /formulario para receber os dados via POST e retorne os mesmos dados (ou uma página HTML com os dados, se preferir):

```python
@app.route('/formulario', methods=['POST'])
def formulario():
    dados_formulario = request.json
    return jsonify(dados_formulario)
```

3 - Certifique-se de que o CORS esteja habilitado em seu servidor Flask para permitir requisições do seu projeto

<h2>Etapa 14: Validando Dados no Front-End com React</h2>
Para validar os dados do formulário no front-end, podemos utilizar o estado do React para armazenar mensagens de erro e condicionalmente exibi-las se houver falhas na validação. Vamos adicionar essa funcionalidade ao nosso componente.

1 - Amplie o estado inicial do seu componente para incluir os erros de validação:

```jsx
const [errors, setErrors] = useState({});
```

2 - Crie uma função para validar os dados antes do envio:

```jsx
const validateForm = (data) => {
    let errors = {};

    if (!data.texto || data.texto.length < 2 || data.texto.length > 255) {
        errors.texto = 'Texto deve ter entre 2 e 255 caracteres.';
    }
    if (!data.inteiro || data.inteiro <= 0 || data.inteiro >= 1000) {
        errors.inteiro = 'Inteiro deve ser maior que 0 e menor que 1000.';
    }
    if (data.booleano === '') {
        errors.booleano = 'Booleano é obrigatório.';
    }
    if (!data.opcaoSelect) {
        errors.opcaoSelect = 'Uma opção do dropdown deve ser selecionada.';
    }
    if (!data.opcaoRadio) {
        errors.opcaoRadio = 'Uma opção de rádio deve ser selecionada.';
    }

    return errors;
}
```

3 - Modifique a função handleSubmit para validar os dados antes do envio. Se houver erros, eles devem ser exibidos ao usuário:

```jsx
    const handleSubmit = (e) => {
        e.preventDefault();
        const formErrors = validateForm(formData);
        if (Object.keys(formErrors).length > 0) {
            setErrors(formErrors);
            return; // Parar a execução se houver erros
        }
        // Se não houver erros, enviar os dados
        axios.post('http://localhost:5000/formulario', formData)
            .then(response => {
                console.log(response.data);
            })
            .catch(error => {
                console.error('There was an error!', error);
            });
    }
```

4 - Adicione mensagens de erro no JSX do formulário, logo abaixo de cada campo de entrada:

```jsx
<div>
    {errors.texto && <p style={{color: 'red'}}>{errors.texto}</p>}
    {/* Repita para os outros campos, ajustando o nome do campo conforme necessário */}
</div>
```

<h2>Etapa 15: Validando Dados no Back-End com Flask</h2>
Para a validação dos dados no back-end, podemos verificar cada campo recebido na requisição POST e retornar uma mensagem de erro se algum dos campos não atender aos requisitos.

1 - Dentro da rota /formulario no Flask, adicione a validação para cada campo:

```python
@app.route('/formulario', methods=['POST'])
def formulario():
    dados = request.json
    erros = {}

    if not dados.get('texto') or len(dados['texto']) < 2 or len(dados['texto']) > 255:
        erros['texto'] = 'Texto deve ter entre 2 e 255 caracteres.'
    if not dados.get('inteiro') or dados['inteiro'] <= 0 or dados['inteiro'] >= 1000:
        erros['inteiro'] = 'Inteiro deve ser maior que 0 e menor que 1000.'
    if 'booleano' not in dados:
        erros['booleano'] = 'Booleano é obrigatório.'
    if not dados.get('opcaoSelect'):
        erros['opcaoSelect'] = 'Uma opção do dropdown deve ser selecionada.'
    if not dados.get('opcaoRadio'):
        erros['opcaoRadio'] = 'Uma opção de rádio deve ser selecionada.'

    if erros:
        return jsonify({"erro": erros}), 400

    return jsonify(dados), 200
```

2 - Certifique-se de que o CORS (Cross-Origin Resource Sharing) esteja habilitado no seu servidor Flask, especialmente se o front-end e o back-end estiverem rodando em portas diferentes. Você pode instalar a extensão Flask-CORS e usá-la em sua aplicação:

```bash
pip install Flask-CORS
```
E no seu app.py, adicione:

```python
from flask_cors import CORS

app = Flask(__name__)
CORS(app)
```

Dessa forma, o servidor Flask validará os dados recebidos do formulário. Se houver algum erro de validação

