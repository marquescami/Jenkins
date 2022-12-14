# Jenkins <img src="https://user-images.githubusercontent.com/31116694/207651940-59711223-f9ff-454a-a082-77fcb27f8faf.png" width="100" height="80" />



## Instruções para executar o projeto:

1) No terminal, acesse: docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk11
2) Vá para o navegador e acesse o endereço: http://localhost:8080/
3) Caso a senha de acesso ao Jenkins não seja exibida no log (Apenas no primeiro acesso), utilize o comando:
"docker logs (D-container" para obter a senha de acesso. (Ex: b2afb7b062d64c90b9770d78af25ff7b)
4) Após inserir a senha na página do jenkins e avançar, selecione a opção: Install Suggested plugins  

![Captura de Tela 2022-12-14 às 13 32 35](https://user-images.githubusercontent.com/31116694/207655795-27be39a5-7d3c-4178-9ea5-e60695cf37db.jpg)

5) Após a finalização, crie um usuário e senha.
6) Ao finalizar a criação do usuário e senha, confirme o endereço informado como localhost.
7) Atualize a página e insira os dados de login para ter acesso a página.

8) Clique em Criar new job

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
  
  11.4) Em Script path:
  jenkins/Jenkinsfile
  
  ![Captura de Tela 2022-12-14 às 16 51 12](https://user-images.githubusercontent.com/31116694/207700966-78c3c642-7979-4530-b696-02bd0878293e.png)
  
  ![Captura de Tela 2022-12-14 às 16 51 30](https://user-images.githubusercontent.com/31116694/207700977-1635b0bd-53f5-4beb-a338-41d1cce55a19.png)
  
  12) Clicar em Construir agora:
   <img width="389" alt="Captura de Tela 2022-12-14 às 16 57 16" src="https://user-images.githubusercontent.com/31116694/207701769-82238b53-3966-4658-b759-9a2657ded431.png">



  
