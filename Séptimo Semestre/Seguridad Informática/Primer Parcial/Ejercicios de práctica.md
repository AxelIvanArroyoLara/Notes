## Snort

Uso de todos los protocolos
TTL 

Diferencia direccion 192.168.5.1 vs 192.168.5.0 (Máquina vs huéspedes de red).

alert tcp any any -> 192.168.10.0/24 80 (
    msg:"Possible command execution attempt";
    flow:to_server,established;
    content:"cmd.exe";
    nocase;
    sid:1000002;
    rev:1;
)

TODOS LOS COMANDOS BASICOS PARA SNORT

Incluir tipos de red