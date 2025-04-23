
---

# Projeto Arduino: Sensor de Luz com LDR

Este projeto tem como objetivo demonstrar o uso de um sensor de luminosidade (LDR) para acionar diferentes LEDs e uma buzina, conforme a intensidade de luz no ambiente. O sistema atua como um indicador de níveis de luminosidade, acendendo LEDs de cores diferentes e ativando uma buzina quando a luz atinge valores críticos.

---

## 👥 Integrantes

- **Arthur Serrano Veloso** – RM: 561542  
- **Hyann dos Santos Espindas** – RM: 563421
- **Theodoro Sievers de Barros Rocha** - RM: 562036
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

## 🔍 Visão Geral do Circuito

O circuito é composto por um sensor LDR ligado a uma das entradas analógicas do Arduino (A0), que mede a intensidade de luz ambiente. A leitura é interpretada pelo código-fonte e, com base no valor:

- **LED verde** acende quando a luminosidade é baixa.
- **LED amarelo** acende quando a luminosidade está em um nível médio, e a **buzina** emite um som a cada 1 segundo.
- **LED vermelho** acende quando a luminosidade é alta, e a **buzina** emite som contínuo sem interrupções.

#### Conexões principais:
- **LDR + resistor de 10kΩ** formam um divisor de tensão, conectado entre 5V, GND e A0.
- **LEDs** conectados aos pinos digitais 13 (verde), 12 (amarelo) e 8 (vermelho), cada um com seu resistor de 220Ω.
- **Buzzer** conectado ao pino digital 7.
- Todos os componentes compartilham o mesmo GND.

---

## 📦 Dependências

Este projeto **não utiliza bibliotecas ou dependências externas**. Todo o código é baseado em funções nativas da linguagem Arduino (C/C++), garantindo simplicidade e fácil execução em qualquer ambiente compatível com a IDE do Arduino.

---

## 🔌 Esquema de Funcionamento

- **LED Verde**: acende quando a luminosidade está baixa (até 600).
- **LED Amarelo**: acende quando a luminosidade está em um nível médio (entre 601 e 801), e a **buzina** faz um som a cada 1 segundo.
- **LED Vermelho + Buzina**: ativam quando a luminosidade é alta (acima de 802), e a **buzina** emite som contínuo sem parar.

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

  // LED Verde acende para luminosidade baixa
  if (valorDaLuz <= 600) {
    digitalWrite(ledPinVerde, HIGH);
  } else {
    digitalWrite(ledPinVerde, LOW);
  }

  delay(100);

  // LED Amarelo acende e buzina toca intermitente para luminosidade média
  if (valorDaLuz > 601 && valorDaLuz <= 801) {
    digitalWrite(ledPinAmarelo, HIGH);
    tone(buzina, 1000);  // Buzina apita a cada 1 segundo
    delay(1000);  // Buzina toca por 1 segundo
    noTone(buzina);  // Desliga a buzina
  } else {
    digitalWrite(ledPinAmarelo, LOW);
  }

  delay(100);

  // LED Vermelho acende e buzina toca continuamente para luminosidade alta
  if (valorDaLuz > 802) {
    digitalWrite(ledPinVermelho, HIGH);
    digitalWrite(buzina, HIGH);  // Buzina emite som contínuo
    tone(buzina, 1000);  // Apito contínuo
  } else {
    digitalWrite(ledPinVermelho, LOW);
    digitalWrite(buzina, LOW);  // Desliga a buzina
  }
}
```

---

## 🧪 Passo a Passo para Reproduzir o Projeto

### 1. Acessar o Projeto
- Clique no link a seguir para abrir o projeto:  
https://www.tinkercad.com/things/3n4SU7639u5-checkpoint-do-arduino-sensor-de-luz?sharecode=76ckdQ39tN1CSJb88PtjC-aVBXon_fwl_4vQ5evZcE0

### 2. Fazer login no Tinkercad
- Caso ainda não tenha uma conta, será necessário criar uma (grátis).
- Se já tiver conta, faça login normalmente.

### 3. Abrir a Simulação
- Após o carregamento do projeto, clique no botão **"Iniciar Simulação"** no canto superior direito da tela.
- Você verá os LEDs e a buzina funcionando de acordo com a intensidade de luz simulada no LDR.

### 4. Alterar a Luminosidade
- Clique sobre o sensor LDR no circuito.
- Ajuste a **barra de valor da luz** para simular diferentes condições de luminosidade.

### 5. Ver o Código
- Clique na aba **"Código"** no canto superior direito para visualizar ou editar o código do Arduino.

### 6. Fazer Alterações (Opcional)
- Você pode modificar o código, os componentes, ou a lógica para personalizar o projeto.
- Para salvar alterações, clique em **"Copiar e Tinker"**.

---
