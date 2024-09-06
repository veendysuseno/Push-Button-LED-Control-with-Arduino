# Push Button LED Control with Arduino

This project demonstrates how to use a push button to control an LED. Each time the button is pressed, the LED toggles between on and off states.

## Components Used

- Arduino Uno
- Push Button (connected to pin 11)
- LED (connected to pin 12)
- Resistor (220Ω recommended for the LED)
- Jumper wires
- Breadboard

## How It Works

- A push button is connected to the Arduino with a pull-up resistor configuration, meaning it reads `HIGH` when not pressed and `LOW` when pressed.
- Each time the button is pressed, the state of the LED changes (on or off).
- A simple debouncing mechanism ensures that the button press is registered only once per press.

## Pin Configuration

- **Push Button**: connected to pin 11 (configured as `INPUT_PULLUP` to ensure reliable readings).
- **LED**: connected to pin 12 (configured as an `OUTPUT`).

## Code Explanation

- In the `setup()` function, the LED pin is set as an output and the button pin is set as an input with the internal pull-up resistor enabled.
- The `loop()` function checks if the button is pressed (`LOW` state). If it is pressed and the button is "ready" (i.e., not already pressed), the LED toggles its state (on or off).
- After the button is pressed, a short delay is used to debounce the button and prevent multiple triggers.

## Code

```cpp
const int PIN_BUTTON = 11;
const int PIN_LED = 12;

bool led_on = false;
bool button_ready = true;

void setup() {
    pinMode( PIN_LED, OUTPUT );
    pinMode( PIN_BUTTON, INPUT_PULLUP );
}

void loop() {
    if( digitalRead(PIN_BUTTON) == LOW && button_ready ) {
        if( led_on ) {
            digitalWrite( PIN_LED, LOW );
            led_on = false;
        } else {
            digitalWrite( PIN_LED, HIGH );
            led_on = true;
        }
        button_ready = false;
    } else if( digitalRead(PIN_BUTTON) == HIGH && !button_ready ) {
        button_ready = true;
    }
    delay( 10 );
}
```

## How to Use

1. Connect the push button and LED to the Arduino as described in the pin configuration.
2. Upload the provided code to the Arduino.
3. Press the button to toggle the LED on and off.

## Features

- Toggles the LED on and off with a push button.
- Uses debouncing to ensure reliable button presses.
- Simple and easy-to-understand project for beginners.

## License

- This project is open-source and can be modified or distributed freely.
