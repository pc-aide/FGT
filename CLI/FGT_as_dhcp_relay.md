````bash
config system interface
    edit "port1"
        set mode dhcp
    next
    edit "port2"
        set ip 0.0.0.0 0.0.0.0
        set allowaccess ping
        set dhcp-relay-service enable
        set dhcp-relay-ip <IP_serveur_DHCP>
    next
    edit "port3"
        set ip 0.0.0.0 0.0.0.0
        set allowaccess ping
        set dhcp-relay-service enable
        set dhcp-relay-ip <IP_serveur_DHCP>
    next
end

````
