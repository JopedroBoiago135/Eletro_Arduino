# Eletro_Arduino
Trabalho II de Eletrônica BCC2023 - Arduino

# Membros
Os integrantes pertencentes a este grupo são:
  - 14675441 - **Henrique Drago** - [HenriqueDrago](https://github.com/HenriqueDrago)
  - 14614564 - **Henrique Yukio Sekido** - [Riquey654](https://github.com/Riquey654)
  - 14681052 - **Arthur Trottmann Ramos** - [ArthurTRamos](https://github.com/ArthurTRamos)
  - 14747211 - **João Pedro Boiago Gomes Santana** - [JopedroBoiago135](https://github.com/JopedroBoiago135)

# Objetivo
O projeto foi baseado na contrução de um circuito em Arduino focado em acender ou apagar um Led de acordo com a frequência de palmas batidas. 

# Componentes Utilizados
| Quantidade | Componentes                        |   Valor R$   |
|------------|------------------------------------|--------------|
| 1          | Módulo Sensor de Som KY-038        |   R$ 00,00   |
| 1          | Led 5mm                            |   R$ 00,50   |
| 10         | Resistor 150 Ω                     |   R$ 00,70   |
| 1          | Arduino UNO R3                     |   R$ 108,0   |
| Total      |                                    |   R$ 00,00   |

# Exemplo Código
```cpp
int microfone = 12;
int led = 8;

int contPalmas = 0;
int palmasLed = 2;

unsigned long tempMaxSom = 500;
unsigned long tempMinSom = 300;
unsigned long compriSonoro = 100;
unsigned long time;
unsigned long startTime = 0;
void setup() {
  pinMode(microfone, INPUT);
  pinMode(led, OUTPUT);
  digitalWrite(led, LOW); //Inicializa o led
}

void loop() {
  time = millis();

  unsigned long tempoAposPalma = time - startTime;

  if(tempoAposPalma >= compriSonoro && digitalRead(microfone) == HIGH) {
    if(tempoAposPalma < tempMinSom || tempoAposPalma > tempMaxSom) {
      contPalmas = 0;
      startTime = millis();
    }
    else {
      contPalmas++;
      startTime = millis();
    }
    if((contPalmas > palmasLed) && (digitalRead(led) == HIGH)) {
      digitalWrite(led, LOW);
      contPalmas = 0;
    }
    if((contPalmas > palmasLed) && (digitalRead(led) == LOW)) {
      digitalWrite(led, HIGH);
      contPalmas = 0;
  }
}
}
```
# Vídeo Simulação

