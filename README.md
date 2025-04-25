
---


# 🌞 Projeto Arduino: Sensor de Luz com LDR

Este projeto demonstra o uso de um sensor de luminosidade (LDR) para acionar diferentes LEDs e uma buzina, conforme a intensidade de luz no ambiente. O sistema atua como um indicador visual e sonoro de níveis de luminosidade.

---

## 👥 Integrantes

- **Arthur Serrano Veloso** – RM: 561542  
- **Hyann dos Santos Espindas** – RM: 563421  
- **Theodoro Sievers de Barros Rocha** – RM: 562036  
- **Leonardo Grosskopf** – RM: 562255  
- **Walter Henrique Pereira de Toledo** – RM: 562476  

---

## 🎯 Objetivo

Utilizar um sensor LDR para medir a intensidade da luz ambiente e acionar:

- LED **verde** quando a luz está **baixa**  
- LED **amarelo** + **buzina intermitente** quando a luz está em **nível médio**  
- LED **vermelho** + **buzina contínua** quando a luz está **alta**

---

## 🧰 Componentes Utilizados

- Arduino Uno  
- Sensor LDR (Light Dependent Resistor)  
- 3 LEDs (verde, amarelo, vermelho)  
- 3 resistores de 220Ω  
- 1 buzina (buzzer ativo)  
- 1 resistor de 10kΩ (para o LDR)  
- Protoboard e jumpers  

---

## 🔌 Esquema de Funcionamento

- **Luminosidade baixa (≤ 600):** LED Verde aceso  
- **Luminosidade média (601 a 801):** LED Amarelo + buzina a cada 1 segundo  
- **Luminosidade alta (> 802):** LED Vermelho + buzina contínua  

---

## 🔧 Conexões

| Componente     | Pino Arduino |
|----------------|--------------|
| LDR + 10kΩ     | A0           |
| LED Verde      | D13          |
| LED Amarelo    | D12          |
| LED Vermelho   | D8           |
| Buzina         | D7           |

---

## 💻 Código-fonte (Simulação)

```cpp
int ledPinVerde = 13;
int ledPinAmarelo = 12;
int ledPinVermelho = 8;
int ldrPin = A0;
int buzina = 7;
int valorDaLuz = 0;

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

  if (valorDaLuz <= 600) {
    digitalWrite(ledPinVerde, HIGH);
  } else {
    digitalWrite(ledPinVerde, LOW);
  }

  delay(100);

  if (valorDaLuz > 601 && valorDaLuz <= 801) {
    digitalWrite(ledPinAmarelo, HIGH);
    tone(buzina, 1000);
    delay(1000);
    noTone(buzina);
  } else {
    digitalWrite(ledPinAmarelo, LOW);
  }

  delay(100);

  if (valorDaLuz > 802) {
    digitalWrite(ledPinVermelho, HIGH);
    tone(buzina, 1000);
  } else {
    digitalWrite(ledPinVermelho, LOW);
    noTone(buzina);
  }
}
```

---

## 🛠 Código-fonte (Projeto Físico Corrigido)

```cpp
int ledPinVerde = 13;
int ledPinAmarelo = 12;
int ledPinVermelho = 8;
int buzina = 7;
int ldrPin = A0;
int valorDaLuz = 0;

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

  // Luminosidade baixa
  if (valorDaLuz <= 600) {
    digitalWrite(ledPinVerde, HIGH);
    digitalWrite(ledPinAmarelo, LOW);
    digitalWrite(ledPinVermelho, LOW);
    noTone(buzina);
  }
  // Luminosidade média
  else if (valorDaLuz <= 801) {
    digitalWrite(ledPinVerde, LOW);
    digitalWrite(ledPinAmarelo, HIGH);
    digitalWrite(ledPinVermelho, LOW);
    tone(buzina, 1000);
    delay(1000);
    noTone(buzina);
  }
  // Luminosidade alta
  else {
    digitalWrite(ledPinVerde, LOW);
    digitalWrite(ledPinAmarelo, LOW);
    digitalWrite(ledPinVermelho, HIGH);
    tone(buzina, 1000);
  }

  delay(200);
}
```

---

## 🧪 Como Testar no Tinkercad

1. Acesse o projeto pelo link:  
   👉 [Simular no Tinkercad](https://www.tinkercad.com/things/3n4SU7639u5-checkpoint-do-arduino-sensor-de-luz?sharecode=76ckdQ39tN1CSJb88PtjC-aVBXon_fwl_4vQ5evZcE0)

2. Faça login (ou crie uma conta gratuita).

3. Clique em **"Iniciar Simulação"**.

4. Ajuste o valor da luz no sensor LDR para testar os diferentes níveis de luminosidade.

5. Acompanhe os LEDs e a buzina funcionando conforme o esperado.

---

## ✅ Observações

- Projeto simples, sem bibliotecas externas.
- Ideal para fins educacionais, aprendizado de sensores e condicionais.
- Pode ser expandido com displays LCD, sensores adicionais ou controle via app.

---
