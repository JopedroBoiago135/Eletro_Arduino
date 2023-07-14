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
| 1          | Módulo Sensor de Som KY-038        |   R$ 17,00   |
| 1          | Led 5mm                            |   R$ 00,50   |
| 10         | Resistor 150 Ω                     |   R$ 00,70   |
| 1          | Arduino UNO R3                     |   R$ 108,0   |
| Total      |                                    |   R$ 126,2   |

# Código Utilizado
```cpp
int microfone = 13; //Entrada digital do KY-038
int led = 8; //Saida do sinal do LED

int contPalmas = 0;
int palmasLed = 0;

unsigned long tempMaxSom = 500;
unsigned long tempMinSom = 300;
unsigned long compriSonoro = 100; //Tempo de espera para o reconhecimento de sons diferentes
unsigned long time;
unsigned long startTime = 0;
void setup() {
  pinMode(microfone, INPUT);
  pinMode(led, OUTPUT);
  digitalWrite(led, HIGH); //Inicializa o led como ligado
}

void loop() {
  time = millis(); //Toma o tempo desde que o arduino foi ligado

  unsigned long tempoAposPalma = time - startTime; //Identifica se o tempo entre 'palmas'

  if(tempoAposPalma >= compriSonoro && digitalRead(microfone) == LOW) {
  //Detecta se o tempo entre 'palmas' foi maior que 100 milisegundos e se o KY-038 detectou um som
    if(tempoAposPalma < tempMinSom || tempoAposPalma > tempMaxSom) {
      contPalmas = 0;
      //Reinicia a contagem se o tempo entre 'palmas' foi curto/longo demais
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

