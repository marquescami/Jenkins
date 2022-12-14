# Jenkins <img src="https://user-images.githubusercontent.com/31116694/207651940-59711223-f9ff-454a-a082-77fcb27f8faf.png" width="100" height="80" />



## Instruções para executar o projeto:

1) No terminal, acesse: docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk11
2) Vá para o navegador e acesse o endereço: http://localhost:8080/
3) Caso a senha de acesso ao Jenkins não seja exibida no log (Apenas no primeiro acesso), utilize o comando:
"docker logs (D-container" para obter a senha de acesso. (Ex: b2afb7b062d64c90b9770d78af25ff7b)
4) Após inserir a senha na página do jenkins e avançar, selecione a opção: Install Suggested plugins  ![Captura de Tela 2022-12-14 às 13 32 35](https://user-images.githubusercontent.com/31116694/207653794-bc22c945-5e96-48bc-bbc8-9ef0fb97d369.png)
5) Após a finalização, crie um usuário e senha.
6) Ao finalizar a criação do usuário e senha, confirme o endereço informado como localhost.
7) Atualize a página e insira os dados de login para ter acesso a página.

