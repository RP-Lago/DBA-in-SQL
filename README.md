# DBA-in-SQL
**Passo a Passo para Criar Usuários no SQL Server**

1. **Abra o Management Studio**: No canto superior esquerdo, clique na pasta "Segurança". Dentro dela, clique na pasta "Logons". Aqui, você encontrará a lista de usuários que podem acessar o SQL Server.

2. **Entenda os Grupos de Usuários**: Existem dois grupos de usuários - os do próprio SQL Server (neste caso, apenas o usuário "sa" que criamos a senha durante a instalação do SQL Server) e os usuários do sistema operacional.

3. **Crie um Usuário do SQL Server**: Na barra de menu superior, clique no botão "Nova Consulta". Em seguida, execute o comando `CREATE LOGIN` seguido do nome do usuário e a senha `WITH PASSWORD = '*******'`.

```sql
CREATE LOGIN user_user WITH PASSWORD = '*******';
```

4. **Teste o Novo Usuário**: No centro inferior da tela, clique no ícone do Management Studio e depois em "SQL Server Management Studio" para abrir outra janela do mesmo studio. Uma janela de login será aberta. No campo de login, digite "user_user" e na senha "*******", depois clique no botão "Conectar".

5. **Verifique o Usuário Conectado**: Minimize essa janela e volte para a do sa. Clique com o botão direito na pasta "Logon" e depois em "Atualizar". O usuário "user_user" deve aparecer na lista.

6. **Crie Usuários do Windows**: No campo de busca do computador, digite "gerenciamento" e clique em "Gerenciamento do computador". Na nova janela, no canto superior esquerdo da tela, clique em "Usuários e Grupos Locais".

7. **Preencha os Campos do Novo Usuário**: Clique com o botão direito na primeira pasta e depois em "Novo usuário". Preencha os campos da seguinte forma:

- Nome de usuário: user_user
- Nome completo: Nome Sobrenome
- Descrição: Programador
- Senha: * * * *
- Confirmar senha: * * * *

Desmarque a opção "O usuário deve alterar a senha no próximo login" e "Conta desativada" e marque "O usuário não pode alterar a senha" e "A senha nunca expira". Clique no botão "Criar" e feche a aba.

8. **Adicione o Usuário ao Grupo**: Na aba Gerenciamento do Computador, clique em "Grupos". Depois, em "Administradores", clique com o botão direito e selecione a opção "Adicionar ao grupo".

9. **Localize o Novo Usuário**: Clique no botão "Adicionar" depois em "Avançado" e "Localizar agora". Uma lista com os usuários será aberta, clique em "user_user". Copie o usuário que aparece como MICRO-DESKTOP\user_user.

10. **Adicione o Usuário ao Sistema Operacional**: Clique no botão "Ok" e depois novamente em "Ok". O usuário user_user foi adicionado ao sistema operacional.

11. **Abra uma Nova Janela do Studio**: Pressione "Shift" e clique com o botão direito em "SQL Server Management Studio", no centro inferior da tela. Depois, clique em "Executar como usuário diferente".

12. **Autentique o Usuário no SQL Server**: Clique no botão "Conectar". Se aparecer uma mensagem de erro dizendo que o usuário user_user não pode se conectar à base de dados, pois não está habilitado para isso, corrija isso na primeira janela que criamos os usuários.

13. **Crie um Novo Login**: Para criar um novo login, escreva `CREATE LOGIN`, em seguida, adicione colchetes. Dentro dele, cole o usuário que salvou no bloco de notas e passe `FROM WINDOWS`.

```sql
CREATE LOGIN [MICRO-DESKTOP\user_user] FROM WINDOWS;
```

14. **Atualize a Lista de Logons**: Após executar, clique com o botão direito na pasta "Logons" e depois em "Atualizar". O usuário deve aparecer na lista de usuários que podem entrar na base de dados.

15. **Conecte-se ao SQL Server com o Usuário do Windows**: Volte para a caixa de diálogo que teve o erro. Clique em "Ok" e depois em "Conectar". Você deve conseguir se conectar ao SQL Server com o usuário user_user do Windows.

Agora você aprendeu como criar um usuário do próprio SQL Server e do Windows. Para continuar com os próximos exercícios, feche a caixa de diálogo do usuário user_user e do usuário.

Funções de Servidor no SQL Server

O SQL Server possui várias funções de servidor que permitem aos usuários gerenciar diferentes aspectos do servidor e dos bancos de dados. Aqui estão algumas dessas funções e suas responsabilidades:

SYSADMIN: Os usuários com essa função têm controle total sobre o servidor e todos os objetos do banco de dados. Eles podem realizar qualquer operação no servidor.

SECURITYADMIN: Essa função permite aos usuários gerenciar funções de servidor, logins e permissões. Eles podem conceder, negar e revogar permissões no servidor.

SERVERADMIN: Os usuários com essa função podem alterar as configurações do servidor e gerenciar o servidor como um todo.

SETUPADMIN: Essa função permite aos usuários gerenciar as instalações do SQL Server. Eles podem adicionar ou remover recursos do SQL Server.

PROCESSADMIN: Os usuários com essa função podem gerenciar processos em execução no servidor. Eles podem terminar processos que estão consumindo muitos recursos.

DISKADMIN: Essa função permite aos usuários gerenciar os discos associados ao SQL Server. Eles podem adicionar ou remover discos do servidor.

DBCREATOR: Os usuários com essa função podem criar, alterar, excluir e restaurar bancos de dados.

BULKADMIN: Essa função permite aos usuários executar operações de importação/exportação em massa e executar operações BULK INSERT.

Além disso, é importante notar que essas funções de servidor são fixas e não podem ser alteradas. Cada função tem um conjunto específico de permissões que não podem ser alteradas. No entanto, você pode adicionar ou remover usuários dessas funções conforme necessário.

Funções de Banco de Dados no SQL Server

O SQL Server possui várias funções de banco de dados que permitem aos usuários gerenciar diferentes aspectos dos bancos de dados. Aqui estão algumas dessas funções e suas responsabilidades:

dbowner: Os membros dessa função têm controle total do banco de dados. Eles podem executar tarefas de gerenciamento de banco de dados, criar, modificar ou excluir objetos do banco de dados e conceder permissões a outros usuários.

db_datareader: Essa função permite aos membros ler qualquer tabela em um banco de dados específico.

db_datawriter: Os membros dessa função têm permissão para modificar dados em qualquer tabela em um banco de dados específico.

db_executor: Essa função permite aos membros executar qualquer procedimento armazenado no banco de dados.

db_ddladmin: Os membros dessa função têm permissão para executar qualquer comando DDL (Data Definition Language) em um banco de dados específico.

db_securityadmin: Essa função permite aos membros gerenciar permissões no banco de dados.

db_accessadmin: Os membros dessa função têm permissão para gerenciar a atribuição de permissões para usuários e funções.

db_backupoperator: Os membros dessa função têm permissão para realizar backups de banco de dados.

db_datareader e db_datawriter: Os membros dessa função combinada têm permissão para ler e modificar dados em qualquer tabela em um banco de dados específico.

Além disso, é importante notar que essas funções de banco de dados são fixas e não podem ser alteradas. Cada função tem um conjunto específico de permissões que não podem ser alteradas. No entanto, você pode adicionar ou remover usuários dessas funções conforme necessário. Isso permite uma gestão eficaz e segura dos bancos de dados
