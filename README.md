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

unsigned long tempMax = 500; //Tempo max entre 'palmas'
unsigned long tempMin = 300; //Tempo min entre 'palmas'
unsigned long espera = 100; //Tempo de espera para o reconhecimento de sons diferentes
unsigned long tempo;
unsigned long startTime = 0;

void setup() {
  pinMode(microfone, INPUT); //Inicializa o pin do microfone como entrada
  pinMode(led, OUTPUT); //Inicializa o pin do LED como saida
  digitalWrite(led, HIGH); //Inicializa o led como ligado
}

void loop() {
  tempo = millis(); //Toma o tempo atual deste ciclo
  //OBS: millis() retorna a quantia de tempo decorrida desde a ativação do sistema

  unsigned long tempAfterPalma = tempo - startTime; //Identifica o tempo entre 'palmas'

  if(tempAfterPalma >= espera && digitalRead(microfone) == LOW) {
  //Detecta se o tempo entre 'palmas' foi maior que 100 milisegundos e se o KY-038 detectou um som
    if(tempAfterPalma < tempMin || tempAfterPalma > tempMax) {
      contPalmas = 0;
      //Reinicia a contagem se o tempo entre 'palmas' foi curto/longo demais
      startTime = millis();
      //Toma o tempo atual como o tempo da ultima palma
    }
    else {
      contPalmas++;
      //Aumenta o contador de 'palmas' se elas forem detectadas dentro do intervalo desejado
      startTime = millis();
      //Toma o tempo atual como o tempo da ultima palma
    }
    if((contPalmas > palmasLed) && (digitalRead(led) == HIGH)) {
      digitalWrite(led, LOW);
      //Se o LED estiver ligado e o contador for atingido, desliga o LED
      contPalmas = 0;
      //Reinicia a contagem
    }
    if((contPalmas > palmasLed) && (digitalRead(led) == LOW)) {
      digitalWrite(led, HIGH);
      //Se o LED estiver desligado e o contador for atingido, liga o LED
      contPalmas = 0;
      //Reinicia a contagem
    }
  }
}
```

# Vídeo do Projeto em Funcionamento

[![Vídeo - Arduino](https://i9.ytimg.com/vi_webp/PcfJkV2sYtg/mq2.webp?sqp=CPj_x6UG-oaymwEmCMACELQB8quKqQMa8AEB-AH-CYAC0AWKAgwIABABGEMgUyhlMA8=&rs=AOn4CLA6LtVWVKkF0Sxnb3YBJvByR56v2g)](https://youtu.be/PcfJkV2sYtg)

# Agradecimentos
- Agradecemos ao [Prof Simões](https://github.com/simoesusp) (vulgo Simas), pelos ensinamentos de eletronica e de como soldar;
- Ao empenho do grupo ao decorrer de todo o trabalho e esforço.

