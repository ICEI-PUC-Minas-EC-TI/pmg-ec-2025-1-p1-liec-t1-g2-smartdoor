# 01 - Introdução

A segurança em ambientes físicos vem evoluindo com a integração de tecnologias modernas de controle de acesso, como fechaduras eletrônicas que utilizam autenticação por reconhecimento facial, biometria, cartões RFID/NFC e gerenciamento remoto. No entanto, o alto custo dessas soluções e a complexidade da infraestrutura necessária tornam sua adoção inviável para muitas empresas, principalmente as de médio porte que buscam alternativas mais acessíveis.

Este projeto apresenta o desenvolvimento de um **protótipo funcional (MVP - Produto Mínimo Viável)** de uma **fechadura eletrônica inteligente** baseada no microcontrolador **ESP32**. Utilizando componentes de baixo custo e bibliotecas open source, o protótipo busca simular um sistema de controle de acesso que seja acessível, escalável e multifuncional — voltado principalmente para fins educacionais, testes em ambientes simples e validação técnica de ideias.

Embora ainda em fase inicial, o projeto demonstra como tecnologias acessíveis podem ser combinadas para simular aplicações reais de automação e controle de acesso, servindo como base para o desenvolvimento de soluções mais robustas no futuro.  A ideia é que, conforme os conhecimentos forem sendo adquiridos ao longo do curso, este protótipo seja gradualmente aprimorado e evoluído até se tornar uma solução com potencial de aplicação profissional.

---

## 🧩 Problema

Sistemas de controle de acesso modernos, quando projetados para ambientes críticos, apresentam **alto custo de implementação inicial**, especialmente quando envolvem múltiplos pontos de entrada e autenticação por biometria, reconhecimento facial ou sistemas remotos integrados. Isso dificulta a adoção em larga escala, principalmente por empresas de médio porte, instituições educacionais e residências que buscam maior segurança com menor investimento.

---

## 🎯 Objetivos

- **Desenvolver um protótipo funcional de controle de acesso** com **baixo custo de implementação**, utilizando o ESP32 e sensores acessíveis.
- **Simular múltiplas formas de autenticação**, como:
  - Cartões ou chaveiros RFID/NFC.
  - Sensor capacitivo (como alternativa simples e interativa).
  - Controle remoto via Bluetooth.
  - Entrada física via botão.
- Exibir mensagens informativas por **display LCD I2C**, com alertas visuais e sonoros.
- Garantir **fechamento automático e feedback ao usuário**.
- Servir como base para **experimentação e aprimoramento gradual**, com foco nas seguintes melhorias futuras:
  - **Desenvolvimento de um aplicativo Android mais completo** para controle remoto e monitoramento.
  - **Criação de uma interface web** para gerenciamento do sistema e visualização de acessos.
  - **Integração com um banco de dados**, para registro de eventos, autenticações e configurações.
  - **Melhorias em autenticação segura**, como uso de senhas, biometria ou criptografia de dados.

---

## 👥 Público-Alvo

O projeto é voltado para:

- **Estudantes e desenvolvedores iniciantes**, interessados em aprender na prática sobre sistemas embarcados, controle de acesso, automação e integração de sensores.
- **Instituições de ensino técnico ou superior**, que desejam demonstrar de forma prática conceitos de eletrônica aplicada, IoT e segurança.
- **Empresas ou indivíduos que buscam simular ou validar soluções de controle de acesso**, antes de investir em tecnologias mais robustas.
- **Residências ou escritórios com necessidade básica de controle de entrada**, onde o protótipo já pode ser aplicado com eficiência.

---

## ⚠️ Observação Importante

Este projeto **não é um produto final pronto para uso profissional**, mas sim um **protótipo educacional**, com foco em aprendizado, experimentação e testes.  
Funciona bem para ambientes simples, como portas de quarto ou espaços com baixo nível de segurança.

Para aplicações mais exigentes — como controle de acesso em ambientes sigilosos, corporativos ou industriais — será necessário o aprimoramento do sistema em aspectos como:

- Autenticação e criptografia seguras.
- Estrutura física reforçada e confiável.
- Aplicativo Android mais completo e funcional.
- Interface web com monitoramento e gerenciamento em tempo real.
- Integração com banco de dados para registros, permissões e auditorias.

**A ideia é transformar este projeto, aos poucos, em uma solução com características profissionais, à medida que novas habilidades forem desenvolvidas ao longo do curso.**

---
