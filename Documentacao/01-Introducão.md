# 01 - Introdução

A segurança em ambientes físicos vem evoluindo com a integração de tecnologias modernas de controle de acesso, como fechaduras eletrônicas que utilizam autenticação por reconhecimento facial, biometria, cartões RFID/NFC e gerenciamento remoto. No entanto, o alto custo dessas soluções e a complexidade da infraestrutura necessária tornam sua adoção inviável para muitas empresas, principalmente as de médio porte que buscam alternativas mais acessíveis.

Este projeto apresenta o desenvolvimento de um **protótipo funcional (MVP - Produto Mínimo Viável)** de uma **fechadura eletrônica inteligente** baseada no microcontrolador **ESP32**. Utilizando componentes de baixo custo e bibliotecas open source, o sistema simula um controle de acesso acessível e multifuncional — com foco em fins educacionais, testes em ambientes simples e validação técnica de ideias.

A proposta é demonstrar, de forma prática, como tecnologias acessíveis podem ser aplicadas em automação e controle de acesso, servindo como base para aprimoramentos futuros conforme o avanço do conhecimento ao longo do curso.

---

## 🧩 Problema

Soluções profissionais de controle de acesso apresentam **alto custo inicial e complexidade**, o que dificulta sua adoção em residências, instituições de ensino ou pequenas empresas. Este projeto busca oferecer uma alternativa de **baixa complexidade e custo reduzido**, ideal para estudo e aplicação em ambientes com menor demanda de segurança.

---

## 🎯 Objetivos

- **Desenvolver um protótipo funcional** de controle de acesso usando ESP32 e sensores acessíveis.
- **Integrar diferentes formas de autenticação**, como:
  - Cartões ou chaveiros RFID/NFC.
  - Sensor capacitivo.
  - Comando remoto via Bluetooth.
  - Botão físico de saída.
- Exibir mensagens no **display LCD I2C**, com **feedback visual (LEDs)** e **sonoro (buzzer)**.
- Simular um **fluxo completo de abertura e fechamento da porta**, com tempo de espera e mensagens ao usuário.
- Estabelecer a base para melhorias futuras.

---

## 👥 Público-Alvo

- **Estudantes e iniciantes** em eletrônica, IoT ou sistemas embarcados.
- **Instituições de ensino** que desejam aplicar práticas reais em sala de aula.
- **Entusiastas de automação residencial** que buscam um ponto de partida para projetos personalizados.
- **Ambientes com baixo nível de segurança**, como quartos, escritórios pessoais ou laboratórios de estudo.

---

## ⚠️ Considerações Finais

Este projeto é um **protótipo educacional**, ideal para aprendizado prático e testes em ambientes com baixo nível de risco.  

Ainda não está pronto para aplicações profissionais ou ambientes críticos. Para isso, serão necessários aprimoramentos em:

- Segurança da autenticação (criptografia, senha, biometria).
- Interface remota (web e mobile).
- Armazenamento e gerenciamento de dados (banco de dados).
- Robusteza física e confiabilidade do hardware.

**A ideia central é evoluir este protótipo gradualmente até se tornar uma solução profissional**, conforme os conhecimentos forem sendo adquiridos ao longo do curso.

---
