# Projeto-Sensor-Luz-CP1
Claro! Aqui está o README atualizado com o código do projeto no Tinkercad:

---

# Projeto Arduino: Sensor de Luz com LDR

Este projeto tem como objetivo demonstrar o uso de um sensor de luminosidade (LDR) para acionar diferentes LEDs e uma buzina, conforme a intensidade de luz no ambiente. O sistema atua como um indicador de níveis de luminosidade, acendendo LEDs de cores diferentes e ativando uma buzina quando a luz atinge valores críticos.

---

## 👥 Integrantes

- **Arthur Serrano Veloso** – RM: 561542  
- **Hyann dos Santos Espindas** – RM: 563421  
- **Theodoro** – RM: *[inserir RM]*  
- **Leonardo Grosskopf** – RM: 562255  
- **Walter Henrique Pereira de Toledo** – RM: 562476  

---

## 🎯 Objetivo

Utilizar um sensor LDR para medir a intensidade da luz ambiente e acionar LEDs com diferentes cores (verde, amarelo e vermelho), além de uma buzina, de acordo com faixas pré-definidas de luminosidade.

---

## 🧰 Componentes Utilizados

- 1 Arduino Uno  
- 1 Sensor LDR (Light Dependent Resistor)  
- 3 LEDs (verde, amarelo e vermelho)  
- 3 resistores (220Ω ou compatíveis para LEDs)  
- 1 buzina (buzzer ativo)  
- 1 resistor de 10kΩ para o LDR  
- Protoboard e jumpers  

---

## 📦 Dependências

Este projeto **não utiliza bibliotecas ou dependências externas**. Todo o código é baseado em funções nativas da linguagem Arduino (C/C++), garantindo simplicidade e fácil execução em qualquer ambiente compatível com a IDE do Arduino.

---

## 🔌 Esquema de Funcionamento

- **LED Verde** acende quando a luminosidade é baixa (até 600).
- **LED Amarelo** acende quando a luminosidade está em um nível médio (entre 601 e 801).
- **LED Vermelho + Buzina** ativam quando a luminosidade é alta (acima de 802).

---

## 💻 Código-fonte

```cpp
int ledPinVerde = 13;
int ledPinAmarelo = 12;
int ledPinVermelho = 8;
int valorDaLuz = 0;
int ldrPin = A0;
int buzina = 7;

void setup() {
  pinMode(ledPinVerde, OUTPUT);
  pinMode(ledPinAmarelo, OUTPUT);
  pinMode(ledPinVermelho, OUTPUT);
  pinMode(buzina, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  valorDaLuz = analogRead(ldrPin);
  Serial.println(valorDaLuz);

  // Luz baixa
  if (valorDaLuz <= 600) {
    digitalWrite(ledPinVerde, HIGH);
  } else {
    digitalWrite(ledPinVerde, LOW);
  }

  delay(100);

  // Luz média
  if (valorDaLuz > 601 && valorDaLuz <= 801) {
    digitalWrite(ledPinAmarelo, HIGH);
  } else {
    digitalWrite(ledPinAmarelo, LOW);
  }

  delay(100);

  // Luz alta
  if (valorDaLuz > 802) {
    digitalWrite(ledPinVermelho, HIGH);
    digitalWrite(buzina, HIGH);
    delay(3000);
    digitalWrite(buzina, LOW);
  } else {
    digitalWrite(ledPinVermelho, LOW);
    digitalWrite(buzina, LOW);
  }
}
```

---

## 📎 Link do Projeto no Tinkercad

🔗 [Acessar Projeto no Tinkercad](https://www.tinkercad.com/things/3n4SU7639u5-checkpoint-do-arduino-sensor-de-luz)

---

Se desejar, posso formatar este conteúdo em PDF ou Word para facilitar a entrega. Gostaria que eu preparasse? 
