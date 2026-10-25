<img width="1920" height="1080" alt="(1) Dylan Li | LinkedIn" src="https://github.com/user-attachments/assets/f3c16147-54f9-4278-8cf5-d0daa8b5b7e3" />

# DisasterChat

Offline messaging for emergencies. Phones connect over Bluetooth and pass messages to each other, so you can reach people with no internet or cell service. Placed 1st out of 20 teams at McMaster's Engineering Competition.

## Why

During disasters, cell towers and internet are often the first things to go down. DisasterChat lets people nearby keep communicating by turning their phones into a network.

## How it works

1. When the app opens, each phone starts advertising and scanning over Bluetooth Low Energy (BLE) and connects to nearby devices automatically.
2. Messages are sent between phones as GATT characteristics.
3. If the person you're messaging isn't in range, nearby phones relay the message forward, up to 5 hops.
4. Each BLE connection reaches about 10 m, but relaying lets messages travel 50 m+. Tested across 4 devices.

react-native-ble-plx only handles scanning and connecting, not advertising, so the advertising side is written as custom Kotlin native modules bridged into React Native.

## Features

- Global chat that broadcasts to every connected device
- One-tap emergency alerts (Help, Medical, Trapped, Flood, Fire, Evacuate)
- Network stats showing connected devices and signal strength
- No accounts, no servers, randomized device IDs

## Tech

React Native, Expo, TypeScript, Kotlin, react-native-ble-plx, Gemma 3 1B (on-device LLM)

```
app/          screens
components/   UI components
modules/      Kotlin native BLE modules
services/     mesh networking and messaging logic
hooks/        React hooks
android/      Android project
```

## Try it

Android 8.0+ with Bluetooth 4.0+ only.

1. Download the [APK](https://drive.google.com/file/d/1PjPtcKWwy9MaAuHsu44lBqkadifdLprh/view?usp=sharing)
2. Download the [Gemma 3 1B model file](https://huggingface.co/litert-community/Gemma3-1B-IT/tree/main) for the on-device LLM
3. Install the APK and allow Bluetooth and location permissions

## Limitations

- Android only
- Continuous BLE uses about 10 to 15% battery per hour
- Devices need to be within about 10 m of at least one other phone in the network
