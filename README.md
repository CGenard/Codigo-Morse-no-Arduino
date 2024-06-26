# Código Morse no Arduino
Código Morse feito na linguagem C, feito para rodar em Arduino.

//Converte caracteres em dados char
caracteres char[] = {'a', 'b', 'c', 'd', 'e', ​​​​'f', 'g', 'h', 'i', 'j', 'k ', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', '0', '1', '2', '3', '4', '5', '6', '7', '8', '9 ', '!', '"', '$', '&', '(', ')', '_', '+', '=', '-', ':', ';', '@ ', '\'', ',', '.', '/', '?', ' '};
char* morse[] = {".-", "-...", "-.-.", "-..", ".", "..-.", "--.", " ....", "..", ".---", "-.-", ".-..", "--", "-.", "---", ".- -.", "--.-", ".-.", "...", "-", "..-", "...-", ".--", "-.. -", "-.--", "--..", "-----", ".----", "..---", "...--", " ....-", ".....", "-....", "--...", "---..", "----.", "-· -·--", "·-··-·", "···-··-", "·-···", "-·--·", "-·--·-", "··--·-", "·-·-·", "-···-", "-····-", "---···", "-·-·-· ", "·--·-·", "·----·", "--··--", "·-·-·-", "-··-·", "··- -··", " "};
int len=55;

//instância em qual pino o buzzer estará localizado
int campainha = 12;

int dotLen = 150; // Você pode ajustar a velocidade dos bipes aqui
int dashLen = pontoLen * 3;
int elemGap = pontoLen;
int charGap = dotLen * 2;
int Espaço = pontoLen * 6;

char charDelimitador = '@'; // Use isto para separar caracteres

String entradaString = "";
booleano stringComplete = false;

configuração vazia() {
 Serial.begin(9600);
 pinMode(buzzerpin, SAÍDA);
 inputString.reserva(200);
}

loop vazio() {
 serialEvent();
 if (stringComplete) {
 Serial.println(inputString); //imprime a mensagem que você escreveu no monitor
 Código de string = toMorse(inputString);
 Exibir(código);
 stringString = "";
 stringComplete = falso;
 }
}

String toMorse(String inputString) {
 inputString.toLowerCase();
 int inputString_len = inputString.length() + 1;
 char char_array[inputString_len];
 inputString.toCharArray(char_array, inputString_len);
 String código final = "";
 for (int i = 0; i < inputString_len; i++) {
 for (int n = 0; n <len; n++) {
 if (char_array[i] == caracteres[n] )
 {
 código final += morse[n];
 código final += charDelimiter;
 }
 }
 }
 retornar código final;
}

String toString(String código) {

 retornar "";
}

void Exibição(Código de string) {
 int code_len = code.length() + 1;
 char código_array[código_len];
 code.toCharArray(code_array, code_len);
 for (int i = 0; i < code_len; i++) {
 if (code_array[i] == '.')
 {

 digitalWrite(buzzerpin, ALTO);
 atraso(pontoLen);

 digitalWrite(buzzerpin, LOW);
 atraso(elemGap);
 Serial.print(code_array[i]);
 }
 senão if (code_array[i] == '-')
 {

 digitalWrite(buzzerpin, ALTO);
 atraso(dashLen);

 digitalWrite(buzzerpin, LOW);
 atraso(elemGap);
 Serial.print(code_array[i]);
 }
 senão if (code_array[i] == ' ')
 {
 atraso(Espaço);
 Serial.print(" ");
 }
 senão if (code_array[i] == charDelimiter)
 {
 atraso(charGap);
 Serial.print(" ");
 }
 }
 Serial.println();
 Serial.println("Pronto");
}
void eventoserial() {
 enquanto (Serial.available()) {
 char inChar = (char)Serial.read();
 inputString += inChar;
 if (inChar == '\n') {
 stringComplete = verdadeiro;
 }
 }
}
