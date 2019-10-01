# Mikrotik Firewall

## Passo a passo para firewall Mikrotik em linha de comando

### Nome das interfaces (interface) (Enter) (print)
>
>set name=INTERNET ethe1
>
> set name=LOCAL ethe2

### Adicionar IP às interfaces (ip address) (Enter) (print)
>
>add address=< end >/< masc > interface=INTERNET
>
>add address=< end >/< masc > interface=LOCAL

### Adicionar DNS (Enter) (ip dns)
>
>set servers=< end >,< end do dns > (Enter) (print)

### Adicionar Rota (ip route) (Enter) 
>
>add gatewall=<end> dst-address=0.0.0.0/0 (Enter) (print)

### Adicionar POOL 
>
>add name=pppoe-pool-< nome do servidor > ranges=< end >- < end > (Enter) (print)

### Adicionar PPP (/ppp) (ppp profile) (Enter) 
>
>add name="perfil-pppoe" use-v j-compression="no" use-mpls="no" use-ipv6="no" use-encryption="no"
use-compression="no" remote-address="pppoe-pool" rate-limit="< limite mínimo >/< limite máximo >" local-address=" < end>"
dns-server="< end >,< end do dns >" dns-change-tcp-nss="yes" (Enter) (print)

### Configurar PPPoE Server (/interface pppoe-server server) (Enter) 
>
>add interface="LOCAL" service-name="pppoe-server-< nome do servidor >" one-session-per-host="yes" disabled="no" 
default-profile="perfil-pppoe" (Enter) (print)

### Adicionar Secret (/ppp) (Enter) (print)

>add nome="nome do servidor  em url " service="pppoe" remote-address="< end >/ < masc >" profile="perfil-pppoe"
password="< insira  sua senha  que deseja>" disabled="no" (Enter) (print)

### Desabilitar Rede Local (ip address) (Enter) (print)
>
>desabled "1" <-- desabilitar Rede Local para não gerar conflito

### Configurar  Firewall NAT (ip firewall nat) (Enter) (print)
>
>add chain="srcnat" out-interface="INTERNET" action="masquerade"