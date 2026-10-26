# Local-LLM-on-microcontroller
Running LLMs locally and accessing on microcontrollers like ESP32.

Connect an ESP32 microcontroller to a locally running Large Language Model (LLM) using Wi-Fi and HTTP. This project explores how embedded systems can interact with locally hosted AI without relying on cloud-based AI APIs.

    The LLM runs on a PC using Ollama, while the ESP32 acts as the embedded client.
    The LLM runs on the PC, not on the ESP32. The ESP32 sends prompts to the local AI server and receives generated responses.


#### Project Goals

    Connect an ESP32 to a local AI inference server.
    Run an LLM locally using Ollama.
    Communicate using HTTP and JSON.
    Build an embedded AI chat interface.
    Develop a Python Flask dashboard.
    Explore AI-assisted robotics and embedded automation. (for later)


### Test Version
    Using Llama 3.2 (1b) model for initial testing.
    ESP32 will run webserver to access the model on local machine.
    The output is printed on ESP32 display (connect OLED)


### Part - 1 PC Setup (windows)

1. Install Ollama
    Windows or macOS: download the installer from https://ollama.com/download and run it. Ollama then runs in the background (tray/menu bar icon).
2. Download a model
    Open a terminal (PowerShell on Windows) and run:ollama pull llama3.2:1b

Test it on the PC first:

    ollama run llama3.2:1b

    Type a message, confirm you get a reply, then exit with /bye.

3. Let other devices (the ESP32) reach it

By default Ollama only listens on the PC itself, so you need to make it listen on the network.

Windows

Quit Ollama from the tray icon (right-click, Quit).
Press the Windows key, search “Edit the system environment variables”, and open it.
Click “Environment Variables”, then “New” under User variables.
Name: OLLAMA_HOST, Value: 0.0.0.0
Click OK, then start Ollama again from the Start menu.

4. Allow it through the firewall
Windows: the first time Ollama listens on the network, Windows may show a firewall prompt. Allow it on Private networks. If there was no prompt, open “Windows Defender Firewall”, then “Advanced settings”, then “Inbound Rules”, then “New Rule”. Choose Port, TCP, 11434, Allow, Private, and give it a name like “Ollama”.
5. Find your PC’s IP address
Windows: run ipconfig and look for the “IPv4 Address” under your WiFi adapter, e.g. 192.168.1.50.

To keep the address from changing, set a DHCP reservation for the PC in your router settings. Otherwise the ESP32 will lose the server whenever the IP changes.

6. Test from another device
On your phone (same WiFi), open http://192.168.1.50:11434 in the browser, using your own IP. If you see “Ollama is running”, the network setup is working.
