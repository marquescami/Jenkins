# Jenkins <img src="https://user-images.githubusercontent.com/31116694/207651940-59711223-f9ff-454a-a082-77fcb27f8faf.png" width="100" height="80" />

Jenkins é um servidor de automação de código aberto independente que pode ser usado para automatizar todos os tipos de tarefas relacionadas à criação, teste e entrega ou implantação de software.

O Jenkins pode ser instalado por meio de pacotes nativos do sistema, Docker ou até mesmo executado de forma autônoma por qualquer máquina com um Java Runtime Environment (JRE) instalado.

##  Instruções para execução do Jenkins no Docker usando o GitHub: 

1) No terminal, acesse: docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk11
2) Vá para o navegador e acesse o endereço: http://localhost:8080/
3) Caso a senha de acesso ao Jenkins não seja exibida no log (Apenas no primeiro acesso), utilize o comando:
"docker logs (D-container" para obter a senha de acesso. (Ex: b2afb7b062d64c90b9770d78af25ff7b)
4) Após inserir a senha na página do jenkins e avançar, selecione a opção: Install Suggested plugins  

![Captura de Tela 2022-12-14 às 13 32 35](https://user-images.githubusercontent.com/31116694/207655795-27be39a5-7d3c-4178-9ea5-e60695cf37db.jpg)

5) Após a finalização, crie um usuário e senha.
6) Ao finalizar a criação do usuário e senha, confirme o endereço informado como localhost.
7) Atualize a página e insira os dados de login para ter acesso a página.

8) Clique em Create a job

![Captura de Tela 2022-12-14 às 16 26 35](https://user-images.githubusercontent.com/31116694/207695375-96030ab9-e900-4c2d-a272-1697af0df785.png)

9) Informe o nome e selecione a opção Pipeline conforme abaixo:

![Captura de Tela 2022-12-14 às 16 31 41](https://user-images.githubusercontent.com/31116694/207697046-5241d678-3ab8-464b-ae05-96223e92ad41.png)

10) Abrirá a página abaixo

<img width="1274" alt="Captura de Tela 2022-12-14 às 16 38 45" src="https://user-images.githubusercontent.com/31116694/207698191-0054983e-f542-4950-adc1-d7dd696a27cf.png">

11) Ir até o final da página e selecionar conforme imagem os items abaixo:

  11.1) Em Pipeline a opção -> Pipeline script from SCM (que pegará um arquivo chamado Jenkinsfile do projeto deste repositório) 
  
  11.2) Em SCM selecionar a opção Git
  
  11.3) Em Repository url inserir a url: 
  https://github.com/marquescami/Jenkins
  
  11.4) No gitHub vá em Settings -> Developer settings (https://github.com/settings/apps)  -> Personal access tokens / Token de acesso pessoal
<img width="1145" alt="Captura de Tela 2022-12-14 às 17 46 22" src="https://user-images.githubusercontent.com/31116694/207710306-a6bfaede-05a0-45b0-aa98-a7154354514e.png">

Marcar a opção -> Public Repositories (read-only) / Repositórios públicos somente leitura
  <img width="874" alt="Captura de Tela 2022-12-14 às 17 47 34" src="https://user-images.githubusercontent.com/31116694/207710524-42f59f88-f6ea-412c-82e0-e7b2d4c9aa47.png">

clique no botão para gerar o token

  <img width="385" alt="Captura de Tela 2022-12-14 às 17 51 28" src="https://user-images.githubusercontent.com/31116694/207711249-d5d14c24-e12f-4e8d-8f6b-d79fbe2fcb81.png">

  11.5) Em credentials configurar conforme abaixo:
  
  <img width="597" alt="Captura de Tela 2022-12-14 às 17 54 25" src="https://user-images.githubusercontent.com/31116694/207712696-2d6b4daf-c5da-44e1-a6f8-d6d341bef650.png">

  
  11.6) Selecionar a credencial criada:

  11.7) Em Script path:
  jenkins/Jenkinsfile
   
  ![Captura de Tela 2022-12-14 às 16 51 30](https://user-images.githubusercontent.com/31116694/207700977-1635b0bd-53f5-4beb-a338-41d1cce55a19.png)
  
  12) Execute no terminar que está rodando o Docker o comando abaixo: 
      sudo chmod 777 /var/run/docker.sock
      
  13) Clicar em Construir agora:
   <img width="389" alt="Captura de Tela 2022-12-14 às 16 57 16" src="https://user-images.githubusercontent.com/31116694/207701769-82238b53-3966-4658-b759-9a2657ded431.png">


##  Exemplos para execução:

### Exemplo 1 -  Clonar o repositório github no script do pipeline do Jenkins e rodar um arquivo de script bash para imprimir hello world

01) Na tela principal do Jenkins, clique em "create a job".
02) Escolha um nome e selecione a opção "pipeline".
03) Na seção Pipeline -> Script insira o código abaixo:

```
  pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git url: 'https://github.com/naiveskill/devops.git', branch: 'main'
                // Change file permisson
                sh "chmod +x -R ./jenkins"
                // Run shell script
                sh "./jenkins/script/scripted_pipeline_ex_2.sh"
            }
        }
    }
}
```
 - Deve ficar desta forma.
<img width="969" alt="Captura de Tela 2022-12-15 às 07 26 17" src="https://user-images.githubusercontent.com/31116694/207835744-0868e8bc-0497-4872-b81e-a776b8b89164.png">


4) Clique em Salvar
5) Clicar em Build now (Construa agora)

### Exemplo 2 - Testando checkout SCM do Git

01) Na tela principal do Jenkins, clique em "create a job".
02) Escolha um nome e selecione a opção "pipeline".
03) Na seção "pipeline" insira o código:

```
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
              checkout([$class: 'GitSCM', 
                branches: [[name: '*/main']],
                doGenerateSubmoduleConfigurations: false,
                extensions: [[$class: 'CleanCheckout']],
                submoduleCfg: [], 
                userRemoteConfigs: [[url: 'https://github.com/naiveskill/devops.git']]])
              sh "ls -ltr"
          }
        }
    }
}
```
4) Clique em Salvar
5) Clicar em Build now (Construa agora)


### Exemplo 3 - Integrando Jenkins com o github

01) Na tela principal do Jenkins, clique em "create a job".
02) Escolha um nome e selecione a opção "pipeline".
03) Em Build Trigger, marque a opção: GitHub hook trigger for GITScm polling

<img width="601" alt="Captura de Tela 2022-12-15 às 07 38 34" src="https://user-images.githubusercontent.com/31116694/207838151-ecd47c8a-1bf9-4543-9f89-4ad3040e7eb5.png">

5) No tópico Pipeline, em definition, altere para: "Pipeline Script from SCM".
	Em SCM, selecione: GIT. Em "Repository url" digite: https://github.com/christianhxc/jenkins-pipeline-tutorial.git
	Em script Path, altere para: hello-world/Jenkinsfile. Em seguida salve as alterações.
  
![Captura de Tela 2022-12-15 às 07 41 58](https://user-images.githubusercontent.com/31116694/207839472-668d475e-997a-45fd-ad57-89d34e5336c2.png)
![Captura de Tela 2022-12-15 às 07 43 27](https://user-images.githubusercontent.com/31116694/207839484-d03a33fe-fc17-4a7d-bcf2-1236bb701139.png)

6) Acesse https://github.com/.... e faça um fork do repositório.
7) Dentro do repositório da aplicação, acesse configurações (Settings). Em seguida, no menu a esquerda, acesse o item: “Webhook” > add webhook.
9) Instalar o ngrok e digitar o comando, no terminal: ngrok http 8080
10) Efetue o login no Github. Na nova tela, em: “Payload Url”, insira: “Ip fornecido pelo ngrok/github-webhook/”.
	Em content type, selecione: application/json. Em seguida clique em add Webhook.
11) Na página principal do Jenkins, clique em Construir agora ou Build Now.
12) O status da compilação será exibido na tela.
A integração já está finalizada com estes passos.
13) No seu diretório do github realize qualquer alteração, como um push ou commit.
14) O jenkins identificará a alteração na página principal.

