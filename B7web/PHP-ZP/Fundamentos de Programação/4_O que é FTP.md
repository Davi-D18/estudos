![[Pasted image 20241115204236.png]]

### O que é FTP?

FTP é um protocolo de rede usado para transferir arquivos entre computadores em uma rede, como a Internet. O FileZilla é um dos clientes FTP mais populares e permite gerenciar conexões FTP de forma fácil e intuitiva.

### 1. **Instalação do FileZilla**

Se você já instalou o FileZilla, pode pular esta etapa. Caso contrário, siga as instruções para instalá-lo em seu sistema operacional usando seu gerenciador de pacotes ou via [site oficial](https://filezilla-project.org/).

### 2. **Conhecendo a Interface do FileZilla**

A interface do FileZilla é dividida em cinco seções principais:

- **Barra de conexão rápida**: permite conectar-se rapidamente a um servidor FTP.
- **Painel de mensagens**: exibe logs das atividades, como conexão e transferência de arquivos.
- **Painel do sistema de arquivos local**: mostra os arquivos e diretórios do seu computador.
- **Painel do sistema de arquivos remoto**: exibe os arquivos e diretórios do servidor.
- **Painel de transferências**: mostra o progresso das transferências em andamento.

### 3. **Como Configurar e Conectar a um Servidor FTP**

#### Conexão Rápida:

1. Na barra de conexão rápida, preencha:
    - **Host**: endereço do servidor (ex.: `ftp.exemplo.com`).
    - **Nome de usuário**: seu nome de usuário do servidor.
    - **Senha**: sua senha de acesso.
    - **Porta**: a porta usada pelo servidor (geralmente `21` para FTP).
2. Clique em **Conexão rápida**.

#### Conexão via Gerenciador de Sites:

1. Vá para **Arquivo > Gerenciador de Sites**.
2. Clique em **Novo Site** e dê um nome para a conexão.
3. Insira os seguintes detalhes:
    - **Host**: endereço do servidor.
    - **Porta**: geralmente `21` para FTP.
    - **Tipo de servidor**: escolha entre **FTP - Protocolo de Transferência de Arquivos** ou **SFTP** se for uma conexão segura.
    - **Tipo de Logon**: escolha entre **Normal**, **Anônimo**, **Solicitar senha**, etc.
    - **Usuário e senha**: preencha se o tipo de logon for **Normal**.
4. Clique em **Conectar**.

### 4. **Transferência de Arquivos**

- **Arrastar e soltar**: você pode arrastar arquivos do painel de sistema de arquivos local para o painel remoto (e vice-versa) para iniciar uma transferência.
- **Menu de contexto**: clique com o botão direito em um arquivo para ver opções como **Carregar**, **Baixar**, **Excluir**, etc.

### 5. **Comandos Úteis**

- **Renomear arquivo/diretório**: clique com o botão direito no arquivo/diretório e selecione **Renomear**.
- **Atualizar a lista de diretórios**: clique com o botão direito em uma área vazia do painel e selecione **Atualizar** para atualizar os arquivos exibidos.
- **Criar nova pasta**: clique com o botão direito no painel e escolha **Criar diretório**.

### 6. **Dicas de Segurança**

- **SFTP em vez de FTP**: sempre que possível, use **SFTP** (FTP sobre SSH) para garantir uma transferência segura dos seus dados.
- **Senhas seguras**: nunca compartilhe suas credenciais de FTP e use senhas fortes para proteger sua conta.
- **Modos ativo e passivo**: em casos de falha na conexão, tente alternar entre **modo ativo** e **modo passivo** nas configurações de conexão.

### 7. **Solução de Problemas Comuns**

- **Erro de autenticação**: verifique se o nome de usuário e senha estão corretos.
- **Problema de permissão**: você pode não ter permissão para acessar ou modificar certos arquivos no servidor. Verifique as permissões do diretório ou entre em contato com o administrador do servidor.
- **Problemas de firewall**: certifique-se de que o firewall local ou o firewall do servidor não está bloqueando a porta de conexão.

### 8. **Recursos Adicionais**

- **Logs detalhados**: o painel de mensagens exibe logs detalhados de todas as atividades, úteis para depuração.
- **Configuração de transferências simultâneas**: em **Editar > Configurações > Transferências**, você pode ajustar o número máximo de transferências simultâneas.