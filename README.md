# 🫀 CardioIA (CardioAssist) - Ecossistema de Saúde IoT

🎥 **Vídeo de Demonstração:** [Assista no YouTube](https://youtu.be/V-josK7Q0TU)

Um ecossistema completo de *Health-Tech* focado em triagem clínica preliminar. O sistema integra hardware IoT para telemetria de sinais vitais em tempo real com um assistente virtual conversacional equipado com Inteligência Artificial para análise de sintomas.

## 🏗️ Arquitetura do Sistema

O projeto adota uma arquitetura em microsserviços dividida em quatro pilares principais:

*   **IoT & Hardware:** Captação de frequência cardíaca via ESP32 (DevKit V4) com comunicação MQTT/WebSocket via HiveMQ. Possui fallback de simulação via hardware (botão BOOT) para contornar falhas de comunicação no barramento I2C.
*   **Backend (API):** Desenvolvido em Python (Flask - `app.py`), atua como orquestrador do sistema, gerenciando requisições, sessões de usuários e integração com o frontend.
*   **Frontend (Dashboard):** Interface reativa em React + Tailwind CSS, apresentando um *split-screen* com chat em tempo real e gráficos de telemetria live (Recharts).
*   **Inteligência Artificial:** 
    *   **IBM Watson Assistant V2:** Máquina de estados avançada para condução do diálogo, triagem de sintomas (dor no peito, falta de ar) e detecção de intenções críticas.
    *   **LLM Local (Ollama/Llama 3.2):** Processamento de linguagem natural local para extração de entidades em dados clínicos não estruturados (`ir_alem_1.py`).

## 🗄️ Persistência de Dados & Monitoramento

*   **SQLite (`pacientes_vitais.db`):** Armazenamento relacional estruturado para os dados de telemetria contínua, gerido e alimentado pelo daemon que assina o broker MQTT (`Ir_alem_2.py`).
*   **TinyDB (NoSQL):** Auditoria em formato JSON para os fluxos do RPA.

## 🚀 Como Executar Localmente

1. Certifique-se de que o motor do modelo de linguagem está ativo (ex: `ollama serve`).
2. Suba o ambiente virtual Python e inicie o backend principal: 
   `python app.py`
3. Em um terminal separado, inicie o assinante do MQTT (responsável por popular o banco de dados): 
   `python Ir_alem_2.py`
4. Para testar o motor de extração generativa clínica isoladamente, execute: 
   `python ir_alem_1.py`
5. Na pasta do frontend, instale as dependências e inicie o painel: 
   `npm install` e depois `npm start`
6. Energize a placa ESP32 (já configurada com credenciais Wi-Fi) para iniciar a transmissão de telemetria no broker público.

---
**👨‍💻 Desenvolvido por:**
Renan

Felipe

Vinicius
