**Title CodeTech IT Solutions Internship - Automatic Room Light Control (IoT Internship)**

**Introduction:**
   In modern homes and offices, efficient use of lighting is crucial for energy conservation and user comfort. Automatic room light control systems leverage IoT technology to adjust lighting based on ambient light levels and user preferences. This documentation outlines the development process and implementation of an automatic room light control system as part of the IoT internship at CodeTech IT Solutions.

**Intern Information**
Name: Anavil Tripathi
Intern ID: ICOD5445

**Task Description**
  This documentation provides an overview of the automatic room light control system developed during the IoT internship at CodeTech IT Solutions. Through this project, I've gained practical experience in IoT development and contribute to the advancement of smart home technology.

**Implementation**
  Implement an Arduino-based system utilizing light sensors to detect ambient light levels, processing the data to determine the required brightness level, and controlling the room lights using light sensor or through potentiometer (handled by the user).
  
```--Code
#include <Adafruit_NeoPixel.h>

#define LED_PIN   9        // Define the pin connected to the NeoPixels
#define NUM_LEDS  32       // Define the number of NeoPixels in the strip

Adafruit_NeoPixel strip(NUM_LEDS, LED_PIN, NEO_GRB + NEO_KHZ800); // Create NeoPixel object

int lightSensorPin = A1;   // Analog pin for the light sensor
int potentiometerPin = A0; // Analog pin for the potentiometer

void setup() {
  strip.begin(); // Initialize the NeoPixel strip
  strip.show();  // Show the initial state (all LEDs off)
  Serial.begin(9600); // Initialize serial communication
}

void loop() {
  // Read analog value from light sensor
  int lightValue = analogRead(lightSensorPin);
  
  // Map the light sensor value (0-1023) to NeoPixel brightness (0-255)
  int brightnessFromLightSensor = map(lightValue, 0, 1023, 255, 0);
  
  // Read analog value from potentiometer
  int potValue = analogRead(potentiometerPin);
  
  // Map the potentiometer value (0-1023) to NeoPixel brightness (0-255)
  int brightnessFromPotentiometer = map(potValue, 0, 1023, 0, 255);
  
  // Determine the minimum brightness from light sensor and potentiometer
  int brightness = min(brightnessFromLightSensor, brightnessFromPotentiometer);
  
  // Set the brightness of the NeoPixel strip
  strip.setBrightness(brightness);
  
  // Define RGB colors for cycling
  uint32_t colors[] = {strip.Color(255, 0, 0),   // Red
                       strip.Color(0, 255, 0),   // Green
                       strip.Color(0, 0, 255)}; // Blue
  int numColors = sizeof(colors) / sizeof(colors[0]); // Calculate the number of colors
  
  // Cycle through the colors
  static int colorIndex = 0; // Static variable to keep track of color index
  for(int i = 0; i < NUM_LEDS; i++) {
    strip.setPixelColor(i, colors[colorIndex]); // Set each pixel to the current color
  }
  strip.show(); // Update the NeoPixel strip with the new colors
  
  colorIndex = (colorIndex + 1) % numColors; // Increment color index for next iteration
  
  delay(1000); // Delay for 1 second to control color change speed
}
```

**Code Explanation:**
- The code includes the necessary library `Adafruit_NeoPixel.h` for controlling NeoPixel LEDs.
- Pins for NeoPixel LED strip, light sensor, and potentiometer are defined.
- In the `setup()` function:
  -> NeoPixel strip is initialized.
  -> Serial communication is initialized for debugging purposes.
- In the `loop()` function:
  -> Analog readings from the light sensor and potentiometer are obtained.
  -> These readings are mapped to the brightness range of NeoPixel LEDs.
  -> The minimum brightness value between the light sensor and potentiometer is selected.
  -> NeoPixel brightness is set accordingly.
  -> RGB colors (Red, Green, Blue) are defined for cycling through the NeoPixel strip.
  -> The color of each pixel in the NeoPixel strip is set to the current color.
  -> NeoPixel strip is updated to display the new colors.
  -> Color index is incremented for cycling through colors.
  -> A delay of 1 second is added to control the speed of color changes.
  
**Conclusion:**
   The automatic room light control system offers several benefits, including energy savings, improved user comfort, and convenience. Through the integration of IoT technology, it provides a smart solution for efficient lighting management in residential and commercial spaces. This project provides valuable hands-on experience in IoT development and contributes to sustainable living practices.

This concludes the documentation for the task "Automatic room light control system" assigned during the CodeTech IT Solutions Internship Program.
