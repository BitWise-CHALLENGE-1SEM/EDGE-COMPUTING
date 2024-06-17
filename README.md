Bruno Biletsky  - RM: 554739

Enrico Ricarte  - RM: 558571

Victor Freire   - RM: 556191

Matheus Gushi   - RM: 556935

# Sistema de Monitoramento e Controle para Carro da Formula E

Este projeto consiste em um sistema embarcado desenvolvido para monitorar e controlar diversos aspectos de um carro de corrida da Formula E, utilizando sensores, um display LCD e LEDs indicativos. O código foi escrito em C++ para a plataforma Arduino.

## Componentes Utilizados

- **Arduino**: Plataforma de desenvolvimento para sistemas embarcados.
- **Sensores**:
  - Sensor DHT22: Utilizado para medir temperatura ambiente.
  - Sensor de luz (A0): Para detectar condições de ativação do modo de ataque.
- **Módulos**:
  - LCD I2C: Display para exibição de informações.
  - RTC DS1307: Módulo para manter a hora e a data atualizadas.
- **LEDs**: Indicam diferentes estados e modos do sistema.
  
## Funcionalidades Principais

### Monitoramento de Temperatura

O sistema monitora continuamente a temperatura ambiente utilizando o sensor DHT22. Dependendo da temperatura medida, o LCD exibe informações sobre o status da temperatura, como "ADEQUADA", "BAIXA", ou "ALTA". Além disso, LEDs indicativos são usados para visualizar rapidamente o estado atual da temperatura.

### Modo de Ataque

O sistema inclui um modo especial de "Attack Mode", que é ativado quando o sensor de luz detecta uma luminosidade acima de um certo limiar por um período específico. Durante o Attack Mode, o LCD exibe um contador regressivo para indicar quanto tempo resta para a desativação automática. Um LED específico pisca para indicar que o modo está ativo.

### Mudança Dinâmica entre Modos

O sistema permite alternar entre diferentes modos de exibição (como "bateria" e "attack_mode") através de um interruptor físico conectado ao pino especificado no código. Cada modo altera as informações exibidas no LCD e o comportamento dos LEDs conforme necessário.

## Configuração e Uso

Para configurar e utilizar este sistema:

1. **Hardware**: Conecte os componentes conforme especificado no código (pino do interruptor, pinos dos LEDs, sensores, etc.).
  
2. **Software**: Carregue o código para a placa Arduino utilizando a IDE Arduino. Certifique-se de ajustar quaisquer configurações necessárias no código, como o UTC_OFFSET para o fuso horário correto.

3. **Funcionamento**: Após carregar o código, o sistema começará a funcionar automaticamente. Use o interruptor para alternar entre os modos de exibição e observe as mudanças no LCD e nos LEDs conforme o ambiente e as condições de corrida mudam.
