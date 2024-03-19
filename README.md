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

2 - Crie um ambiente virtual: Para manter as dependências do projeto isoladas, é uma boa prática usar um ambiente virtual. Crie um para o seu projeto Flask:

```bash
python3 -m venv myprojectenv
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

2 - Crie um novo projeto React: Com o Node.js instalado, você pode criar um novo projeto React:

```bash
npx create-react-app my-react-app
cd my-react-app
npm start
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

1 - Crie um diretório para o seu projeto Flask e entre nele:

```bash
mkdir meu_projeto_flask
cd meu_projeto_flask
```

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

1 - Crie um novo aplicativo React usando o Create React App, uma ferramenta oficialmente suportada que cria um front-end React com uma boa configuração padrão. Substitua meu-app-react pelo nome que desejar para seu aplicativo:

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

