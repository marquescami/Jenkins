# Jenkins <img src="https://user-images.githubusercontent.com/31116694/207651940-59711223-f9ff-454a-a082-77fcb27f8faf.png" width="100" height="80" />


Jenkins é um servidor de automação de código aberto independente que pode ser usado para automatizar todos os tipos de tarefas relacionadas à criação, teste e entrega ou implantação de software.

O Jenkins pode ser instalado por meio de pacotes nativos do sistema, Docker ou até mesmo executado de forma autônoma por qualquer máquina com um Java Runtime Environment (JRE) instalado.

Documentação oficial 
https://www.jenkins.io/doc/

##  Instruções para execução do Jenkins no Docker usando o GitHub: 

1) No terminal, acesse: docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk11
2) Vá para o navegador e acesse o endereço: http://localhost:8080/
3) Caso a senha de acesso ao Jenkins não seja exibida no log (Apenas no primeiro acesso), utilize o comando:
"docker logs (ID-container" para obter a senha de acesso. (Ex: b2afb7b062d64c90b9770d78af25ff7b)
4) Após inserir a senha na página do jenkins e avançar, selecione a opção: Install Suggested plugins  

![Captura de Tela 2022-12-14 às 13 32 35](https://user-images.githubusercontent.com/31116694/207655795-27be39a5-7d3c-4178-9ea5-e60695cf37db.jpg)

5) Após a finalização, crie um usuário e senha.
6) Ao finalizar a criação do usuário e senha, confirme o endereço informado como localhost.
7) Atualize a página e insira os dados de login para ter acesso a página.


##  Exemplos para execução do Jenkins

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

 - Deve ficar desta forma.
 
 <img width="972" alt="Captura de Tela 2022-12-15 às 08 42 16" src="https://user-images.githubusercontent.com/31116694/207850661-1399ecd0-f637-463a-9cd7-fff0fbdaf0ea.png">

4) Clique em Salvar
5) Clicar em Build now (Construa agora)


# Continue aprendendo sobre o Jenkins

Integrando o Jenkins com o github

01) Na tela principal do Jenkins, clique em "create a job".
02) Escolha um nome e selecione a opção "pipeline".
03) Em Build Trigger, marque a opção: GitHub hook trigger for GITScm polling

<img width="601" alt="Captura de Tela 2022-12-15 às 07 38 34" src="https://user-images.githubusercontent.com/31116694/207838151-ecd47c8a-1bf9-4543-9f89-4ad3040e7eb5.png">

5) No tópico Pipeline, em definition, altere para: "Pipeline Script from SCM".
	Em SCM, selecione: GIT. Em "Repository url" digite: https://github.com/marquescami/Jenkins
	Em script Path, altere para: hello-world/Jenkinsfile. Em seguida salve as alterações.
	
  <img width="921" alt="Captura de Tela 2022-12-15 às 08 31 48" src="https://user-images.githubusercontent.com/31116694/207848979-71a7b39a-9155-4a53-99a8-77765df6b415.png">

![Captura de Tela 2022-12-15 às 07 43 27](https://user-images.githubusercontent.com/31116694/207839484-d03a33fe-fc17-4a7d-bcf2-1236bb701139.png)

6) Acesse esse repositório https://github.com/marquescami/Jenkins e faça um fork do repositório.
7) Dentro do repositório GitHub da aplicação, acesse configurações (Settings). Em seguida, no menu a esquerda, acesse o item: “Webhook” > add webhook.

<img width="1118" alt="Captura de Tela 2022-12-15 às 08 35 01" src="https://user-images.githubusercontent.com/31116694/207849465-48d1e916-b5ae-40dd-a5a3-4b032815a3d4.png">

<img width="820" alt="Captura de Tela 2022-12-15 às 08 39 07" src="https://user-images.githubusercontent.com/31116694/207850263-ac97d3c7-0b68-4b87-8f43-6e023051b36d.png">

9) Instalar o ngrok (https://ngrok.com/download) e digitar o comando, no terminal: ngrok http 8080
10) Efetue o login no Github. Na nova tela, em: “Payload Url”, insira: “Ip fornecido pelo ngrok/github-webhook/”.
	Em content type, selecione: application/json. Em seguida clique em add Webhook.
11) Na página principal do Jenkins, clique em Construir agora ou Build Now.
12) O status da compilação será exibido na tela.
A integração já está finalizada com estes passos.
13) No seu diretório do github realize qualquer alteração, como um push ou commit.
14) O jenkins identificará a alteração na página principal.


