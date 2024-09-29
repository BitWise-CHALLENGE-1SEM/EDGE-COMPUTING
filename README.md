Bruno Biletsky   - RM: 554739

Enrico Ricarte   - RM: 558571

Victor Freire    - RM: 556191

Matheus Gushi    - RM: 556935

Pedro Ferrari    - RM: 554887

# Sistema de Monitoramento e Controle para Carro da Formula E

Este projeto consiste em um sistema embarcado desenvolvido para monitorar  e controlar (localmente e à distancia) diversos aspectos de um carro de corrida da Formula E, utilizando a plataforma FIWARE para enviar os dados à NUVEM (para acessá-los de qualquer lugar), sensores, um display LCD e LEDs indicativos. O código foi escrito em C++ para a plataforma Arduino.

## Componentes Utilizados
- **Plataforma FIWARE**:  Plataforma de infraestrutura aberta que será utilizada para captar e armazenar dados de temperatura e luminosidade dos sensores (permitindo acessar os dados de qualquer lugar a qualquer momento)
- **Serviço de computação em NUVEM**: Amazon Web Services (AWS)
- **ESP32**: Plataforma de desenvolvimento para sistemas embarcados com WI-FI integrado.
- **Sensores**:
  - Sensor DHT22: Utilizado para medir temperatura ambiente.
  - Sensor de luz (A0): Para detectar condições de ativação do modo de ataque.
- **Módulos**:
  - LCD I2C: Display para exibição de informações.
  - RTC DS1307: Módulo para manter a hora e a data atualizadas.
- **LEDs**: Indicam diferentes estados e modos do sistema.
  
## Funcionalidades Principais

### Envio de Dados em Tempo Real para a Nuvem 

![bitwise_diagrama_fiware](https://github.com/user-attachments/assets/a3dc91eb-b904-4c91-b249-e9147806a2fa)

#### Descrição do Sistema
Todos os dados de temperatura e luminosidade captado pelo sistema é enviado em tempo real para a nuvem, utilizando a plataforma FIWARE. Esta funcionalidade é essencial para monitorar e analisar as condições do carro de corrida remotamente.

#### Como a Plataforma FIWARE Funciona
A plataforma FIWARE é uma infraestrutura aberta que facilita a criação de aplicações inteligentes em diversas áreas, incluindo a Internet das Coisas (IoT). No contexto deste projeto, FIWARE é utilizada para captar e armazenar dados de temperatura e luminosidade dos sensores, sendo assim, através do POSTMAN podemos acessar em tempo real os dados captados pelos sensores, além de posteriormente possibilitar a criação de gráficos (dashboard histórico) para analisar os dados captados durante uma corrida ou até mesmo para verificá-los em tempo real através de um dashboard dinâmico.

#### Envio para a Nuvem
1. **Conexão**: O ESP32 se conecta à internet através de um módulo Wi-Fi ou Ethernet.

2. **Protocolo**: Utilizando protocolos como MQTT, os dados são enviados para o FIWARE Orion Context Broker.

#### Armazenamento e Processamento
1. **Orion Context Broker**: Este componente central do FIWARE recebe os dados e os armazena como entidades contextuais.

2. **Persistência**: Para armazenamento a longo prazo, os dados são enviados para um banco de dados MongoDB.

#### Análise e Visualização
**Ferramentas de Análise**: Após as informações serem armazenadas no MongoDB, podemos utilizar outras ferramentas para a coleta de dados históricos e a representação deles em dashboards estáticos (dados históricos) ou dinâmicos (atualizado em tempo real). Nesse contexto, utilizamos o Google Colaboratory (Python) para gerar o dashboard histórico.

### Monitoramento de Temperatura

O sistema monitora continuamente a temperatura ambiente utilizando o sensor DHT22. Dependendo da temperatura medida, o LCD exibe informações sobre o status da temperatura, como "ADEQUADA", "BAIXA", ou "ALTA". Além disso, LEDs indicativos são usados para visualizar rapidamente o estado atual da temperatura.

### Modo de Ataque

O sistema inclui um modo especial de "Attack Mode", que é ativado quando o sensor de luz detecta uma luminosidade acima de um certo limiar por um período específico. Durante o Attack Mode, o LCD exibe um contador regressivo para indicar quanto tempo resta para a desativação automática. Um LED específico pisca para indicar que o modo está ativo.

### Mudança Dinâmica entre Modos

O sistema permite alternar entre diferentes modos de exibição (como "bateria" e "attack_mode") através de um interruptor físico conectado ao pino especificado no código. Cada modo altera as informações exibidas no LCD e o comportamento dos LEDs conforme necessário.

## Configuração e Uso

Para configurar e utilizar este sistema:

1. **Hardware**: Conecte os componentes conforme especificado no código (pino do interruptor, pinos dos LEDs, sensores, etc.).
  
2. **Software**: Crie um sistema FIWARE utilizando um serviço de CLOUD COMPUTING da usa preferência, nós utilizamos Amazon Web Services (AWS), para poder captar os dados dos sensores e armazená-los em um banco de dados. Carregue o código para a placa ESP32 utilizando a IDE Arduino. Certifique-se de ajustar quaisquer configurações necessárias no código, como o UTC_OFFSET para o fuso horário correto e as configurações de login e senha da sua coneção com a internet.

3. **Funcionamento**: Após carregar o código, o sistema começará a funcionar automaticamente. Use o interruptor para alternar entre os modos de exibição e observe as mudanças no LCD e nos LEDs conforme o ambiente e as condições de corrida mudam, além de poder, através de uma API, acessar os dados enviados para sua plataforma FIWARE e trabalhar com os dados contidos no MongoDB.
