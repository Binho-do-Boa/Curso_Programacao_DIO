# Repositório de Desafios de Programação e Segurança

Bem-vindo ao meu repositório de desafios! Aqui, organizo os projetos e códigos desenvolvidos como parte dos cursos e desafios da DIO (Digital Innovation One). Cada desafio é documentado com detalhes sobre o problema, a solução implementada, os arquivos relacionados e as lições aprendidas. Este repositório serve como um portfólio do meu aprendizado em programação e segurança da informação.

O foco principal é demonstrar a aplicação prática de conceitos aprendidos, com códigos comentados, capturas de tela e recomendações de boas práticas. Sinta-se à vontade para explorar, clonar e testar os projetos!


## Desafio 01
Em sistemas de autenticação segura, é comum bloquear contas após múltiplas tentativas de login inválidas consecutivas. Esse mecanismo evita ataques de força bruta e protege a conta do usuário. Neste desafio, você deverá verificar uma lista de tentativas de login e identificar se a conta deve ser bloqueada com base em tentativas falhas seguidas.
Uma conta deve ser bloqueada se houver 3 ou mais tentativas consecutivas de falha.

## Desafio 02
Em cibersegurança, é fundamental monitorar a entrada de dados fornecidos pelo usuário para prevenir injeção de comandos. Comandos maliciosos podem ser executados no sistema, comprometendo sua segurança. Neste desafio, você deve criar uma lógica para identificar se um comando fornecido pelo usuário contém caracteres que possam ser usados para realizar injeções de comandos.
O objetivo é identificar se o comando fornecido contém caracteres frequentemente utilizados para executar múltiplos comandos de forma encadeada ou maliciosa. A seguir, você encontrará as regras de detecção e os critérios para marcar um comando como suspeito: O comando será considerado suspeito se contiver qualquer um dos seguintes caracteres: ;, &, |, ou $. Se o comando contiver qualquer um desses caracteres, será considerado suspeito e o sistema deve alertar sobre um possível risco de injeção de comando. Com isso, o sistema deve garantir que comandos potencialmente maliciosos sejam identificados, alertando os usuários ou equipes de segurança sobre tentativas de exploração do sistema.

## Desafio 03
Você deverá implementar, documentar e compartilhar um projeto prático utilizando Python, simulando o comportamento de malwares em um ambiente seguro.   

**Keylogger Simulado:** Programar captura de teclas em arquivo .txt, torná-lo mais furtivo e implementar envio automático por e-mail.   

**Ransomware Simulado:** Criar arquivos de teste, implementar um script que criptografa e descriptografa, além de gerar mensagem de “resgate”.  

** Trojan com formulario Bancario:** Criar um trojan para aparecer apresentar uma tela para usuario colocar usuario e senha e o mesmo ser enviado por email para atacante.

