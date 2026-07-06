# Laboratorio: Análisis Forense de Red - Detección de RAT (NetSupport Manager) 

Este repositorio documenta la investigación técnica de un incidente de compromiso de red mediante el análisis profundo de paquetes (DPI) utilizando Wireshark.

##  Resumen del Incidente
Se detectó un comportamiento anómalo en un equipo de la red interna que realizaba conexiones repetitivas hacia un servidor externo. La investigación confirmó la presencia de tráfico asociado a herramientas de acceso remoto no autorizadas (RAT).

##  Hallazgos Forenses

- **IP de la Víctima:** `10.2.28.88` (Identificada por el alto volumen de tráfico con 14,673 paquetes en los Endpoints).
- **IP del Atacante / Servidor C2:** `45.131.214.85`
- **Indicador de Compromiso (IoC) Clave:** Conexiones continuas vía HTTP POST hacia `/fakeurl.htm`.
- **Firma del Artefacto (User-Agent):** `NetSupport Manager/1.3` operando a través del puerto 80.
- **Análisis del Flujo (TCP Stream 40):** Se identificó el intercambio de comandos de control en texto plano (`CMD=POLL`, `CMD=ENCD`) y payloads de datos sospechosos, confirmando la persistencia del atacante en el host.
- ![Endpoints de Wireshark](dirección%20IP.png)
![Tráfico HTTP Malicioso](direccion%20web%20atacante.png)
![Tráfico HTTP Malicioso](direccion%20web%20atacante.png)
![Objetos Exportados](paquete%20sospechoso.png)
## 🛠️ Mitigación Recomendada (Blue Team)
1. **Aislamiento:** Desconectar inmediatamente el host `10.2.28.88` de la red local para evitar movimientos laterales.
2. **Bloqueo Perimetral:** Crear una regla de salida persistente en el Firewall para denegar cualquier comunicación hacia la IP `45.131.214.85`.
3. **Remediación:** Realizar un escaneo exhaustivo y auditoría de procesos en el host afectado para remover binarios de NetSupport no autorizados.
