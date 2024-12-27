//Example-of-Sending-a-Signal-Using-nRF24L01-Receiver-Code-Arduino-2-
#include <SPI.h>
#include <nRF24L01.h>
#include <RF24.h>

RF24 radio(9, 10);  // CE pin 9, CSN pin 10
const byte address[6] = "00001";  // Address for communication

void setup() {
  Serial.begin(9600);
  radio.begin();
  radio.openReadingPipe(0, address);  // Open the reading pipe
  radio.setPALevel(RF24_PA_MIN);      // Set power level to low
  radio.startListening();             // Start listening for messages
}

void loop() {
  if (radio.available()) {
    char text[32] = {0};
    radio.read(&text, sizeof(text));  // Read the incoming message
    Serial.println(text);  // Print the received message
  }
}

