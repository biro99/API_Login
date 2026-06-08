API de Gerenciamento de Corrida e Usuários (api_login)
Este documento explica de forma simples como a nossa API foi feita, mostrando as tecnologias que usamos, como as pastas estão organizadas e o que o sistema consegue fazer.

1. Tecnologias Utilizadas
Para criar o sistema, usamos o Node.js junto com as seguintes ferramentas:

Express: Cria o servidor da nossa API e cuida de receber os pedidos (como listar ou cadastrar algo) e enviar as respostas de volta.
MySQL2: Conecta o nosso código Node.js diretamente ao banco de dados MySQL para que possamos salvar e buscar as informações de forma rápida.
Nodemon: Facilita o trabalho na hora de programar, pois reinicia o servidor sozinho toda vez que salvamos um arquivo.
Dotenv: Esconde as senhas do banco de dados e as portas do sistema em um arquivo separado (.env) por motivos de segurança.
Cors: Libera e protege o acesso para que o nosso sistema de Front-End consiga conversar com a nossa API sem bloqueios de segurança.

2. Estrutura do Sistema
O projeto é organizado dividindo as responsabilidades de cada arquivo para que o código não fique bagunçado:
Na raiz do projeto, temos o arquivo package.json que lista as ferramentas instaladas, e o arquivo oculto .env que guarda as senhas e acessos. O arquivo server.js serve apenas para ligar o servidor e deixar a API rodando na porta correta.
A configuração principal fica no arquivo app.js. É ele quem ativa o CORS, faz a API entender textos no formato JSON e puxa as rotas de cada parte do sistema. Já a conexão com o banco de dados fica isolada no arquivo db.js, que testa se o MySQL está funcionando assim que o servidor liga.
Por fim, dentro da pasta routes, dividimos os caminhos do sistema: o arquivo user.js cuida do que acontece em '/usuarios', o corredor.js cuida de '/corredores' e o voltas.js controla as requisições enviadas para '/voltas'.

3. Funcionalidades Implementadas
O sistema foi feito para controlar o cadastro de usuários e marcar os tempos e o desempenho de corridas (como Kart ou Atletismo). Ele faz o seguinte:

A) Parte de Usuários e Segurança (/usuarios)
Cuida das pessoas que vão mexer no sistema e garante a segurança dos acessos:
Cadastro de Usuários: Salva novos usuários transformando as senhas em códigos seguros usando a ferramenta bcrypt, para que ninguém consiga ver a senha real no banco de dados.
Login e Autenticação: Verifica se o usuário e a senha estão certos e gera um token seguro (JWT) para dar permissão de acesso ao sistema.

B) Parte de Corredores (/corredores)
Gerencia os pilotos ou atletas da corrida:
Controle de Atletas: Permite cadastrar, ver a lista, atualizar os dados e apagar corredores do sistema (nome, número, equipe, etc.).

C) Parte de Voltas (/voltas)
Marca o tempo e os dados de desempenho na pista:
Registro de Tempos: Salva os tempos de cada volta e a velocidade de um corredor específico.
Histórico de Desempenho: Mostra relatórios para ver quem correu mais rápido por atleta ou por dia de corrida.

D) Teste de Funcionamento (/test)
Teste de Conexão: Uma rota simples que responde apenas um "OK" em formato JSON para o programador testar se o servidor está ligado e funcionando perfeitamente.
