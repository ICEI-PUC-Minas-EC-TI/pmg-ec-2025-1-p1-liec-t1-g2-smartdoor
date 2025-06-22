## Testes do Projeto

Os testes do projeto foram conduzidos principalmente pelo Scrum Master (Gabriel Campos), que também foi responsável pelo desenvolvimento completo do código e da montagem do hardware.

### Estratégia de Testes

- A abordagem adotada foi testar **individualmente cada componente** com sua biblioteca padrão.
- Após garantir o funcionamento de cada módulo de forma isolada (por exemplo, RFID, display LCD, buzzer, servo motor), os componentes foram sendo **integrados gradualmente**.
- A cada nova integração, o sistema era novamente testado para garantir que os módulos estavam funcionando em conjunto sem conflitos.
- Quando a integração parcial apresentava funcionamento estável, novos elementos eram adicionados até que todo o protótipo estivesse finalizado e funcional.

### Testes do Hardware

- Todos os testes de hardware foram realizados diretamente no protótipo final montado em protoboard.
- O funcionamento do RFID foi validado com três UIDs autorizados diferentes.
- O sensor capacitivo foi testado com toques manuais e funcionou de maneira consistente após três toques consecutivos.
- O servo motor foi testado simulando a abertura e o fechamento da porta.
- LEDs e buzzer foram acionados em diferentes estados do sistema, garantindo feedback sonoro e visual ao usuário.
- A alimentação por USB apresentou estabilidade durante os testes.

### Testes do Aplicativo

- Como o desenvolvimento do aplicativo não foi concluído em tempo hábil, os testes de comunicação Bluetooth foram realizados utilizando o aplicativo **"Bluetooth Serial Terminal"** para Android.
- Esse app foi utilizado para **simular os comandos** de abertura (`'1'`) e fechamento (`'2'`) da porta.
- A comunicação entre o app e o ESP32 se mostrou estável, com resposta imediata do sistema aos comandos enviados.
- O feedback visual (display LCD e LEDs) e sonoro (buzzer) confirmava que os comandos estavam sendo interpretados corretamente pelo ESP32.
