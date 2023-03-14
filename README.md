#Sensor de nível

Sensores de Nível, também conhecidos como “chave de nível” ou “bóia de nível“, funcionam com contato reed switch e flutuador magnético. O movimento desse flutuador abre ou fecha o contato do reed switch.

 Sensor de nível de água

O sensor de Nível de Água possibilita aos projetos integrados, controlar o nível de água nos mais diversificados reservatórios. Como os reservatórios estão comumente instalados em locais altos e de difícil acesso fica complicado controlar sua quantidade de água. Nestes casos o Sensor de Nível torna-se indispensável para facilitar e proporcionar melhores experiências à quem utiliza desta estrutura.

Sensor De Nível De Água Com Boia Horizontal:

O sensor de nível de água é um equipamento com diversos modelos, todos com suas especificações e características próprias. A principal diferença está em seu método de verificação com boia que pode ser tanto horizontal quanto vertical. Tendo em vista o local de instalação e seu funcionamento neste projeto, optamos pelo Sensor de Nível com Boia Horizontal.

![image](https://user-images.githubusercontent.com/127752577/224996691-bd9dc9c3-4d27-416b-8c55-f43942c14422.png)

O funcionamento deste equipamento é extremamente simples uma vez que conta com apenas dois fios para sua comunicação e acionamento. O sinal para detecção junto ao Arduino é gerado através de um Reed Switch e um imã, um instalado na base e outro na boia.

 Produtos Utilizados no Projeto:
 
– 5 Sensores de Nível de Água com Boia Horizontal;

– 1 Arduino UNO + Cabo USB;

– 5 Resistores 10K ¼W;

– Protoboard e Jumpers;

– Display LCD 16×2 com fundo azul;

– Módulo Adaptador I2C (IIC).

 Esquema de Ligação do Sensor de Nível de Água sem Display
O esquema de ligação deste projeto é tão simples quanto o funcionamento do Sensor de Nível de Água. O que dificulta a ligação é a utilização de cinco sensores de nível e a necessidade de resistores Pull Down. Os resistores são responsáveis por evitar a oscilação do sinal de nível lógico estabelecendo um nível LOW como padrão.

![image](https://user-images.githubusercontent.com/127752577/224997234-9dd0a89f-f230-43d4-9190-43b84e8cc044.png)

![image](https://user-images.githubusercontent.com/127752577/224997326-826c2da8-fd96-4efd-bf95-c34e14967ba7.png)

Código de Funcionamento do Sensor de Nível de Água:


// Código de Verificação para Nível de Água
// Arduino IDE Versão 1.8.13
// Exemplo de visualização no Monitor Serial
 
#define Sensor1 7
#define Sensor2 8
#define Sensor3 9
#define Sensor4 10
#define Sensor5 11
#define rele    13
 
int sensor1 = 1, sensor2 = 1, sensor3 = 1, sensor4 = 1, sensor5 = 1;
 
int nivelinicial = 0;
 
void setup() {
 
  Serial.begin(9600);
 
  pinMode(Sensor1, INPUT);
  pinMode(Sensor2, INPUT);
  pinMode(Sensor3, INPUT);
  pinMode(Sensor4, INPUT);
  pinMode(Sensor5, INPUT);
  pinMode(rele,    OUTPUT);
 
  Serial.println("Nivel do Reservatorio");
  Serial.println();
}
 
void loop() {
  int sensor1 = digitalRead(Sensor1);
  int sensor2 = digitalRead(Sensor2);
  int sensor3 = digitalRead(Sensor3);
  int sensor4 = digitalRead(Sensor4);
  int sensor5 = digitalRead(Sensor5);
 
  if ((sensor1 == 1) && (sensor2 == 1) && (sensor3 == 1) && (sensor4 == 1) && (sensor5 == 1)) {
    Serial.println("Reservatorio Cheio");
    digitalWrite(rele, LOW);
  }
 
  else if ((sensor1 == 1) && (sensor2 == 1) && (sensor3 == 1) && (sensor4 == 1) && (sensor5 == 0)) {
    Serial.println("Nivel de 100 a 75%");
  }
 
  else if ((sensor1 == 1) && (sensor2 == 1) && (sensor3 == 1) && (sensor4 == 0) && (sensor5 == 0)) {
    Serial.println("Nivel de 75 a 50%");
  }
 
  else if ((sensor1 == 1) && (sensor2 == 1) && (sensor3 == 0) && (sensor4 == 0) && (sensor5 == 0)) {
    Serial.println("Nivel de 50 a 25%");
  }
 
  else if ((sensor1 == 1) && (sensor2 == 0) && (sensor3 == 0) && (sensor4 == 0) && (sensor5 == 0)) {
    Serial.println("Nivel Critico");
      digitalWrite(rele, HIGH);
  }
 
  else if ((sensor1 == 0) && (sensor2 == 0) && (sensor3 == 0) && (sensor4 == 0) && (sensor5 == 0)) {
    Serial.println("Reservatorio Vazio");
  }
 
  else {
    Serial.println("ALERTA - ERRO");
  }
 
  delay(1000);
}
