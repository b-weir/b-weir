version: '3.3'
services:
    transmission-openvpn:
        cap_add:
            - NET_ADMIN
        volumes:
            - /mnt/blackmedia/Torrent:/data
            - /home/docker/torrentdata/transmission:/config
        environment:
            - OPENVPN_PROVIDER=PIA
            ## Use the Switzerland VPN
            - OPENVPN_CONFIG=switzerland
            ## Add Username for PIA
            - OPENVPN_USERNAME=
            ## Add password for PIA
            - OPENVPN_PASSWORD=
            - LOCAL_NETWORK=192.168.101.0/24
            - TRANSMISSION_SPEED_LIMIT_UP_ENABLED=true
            - TRANSMISSION_SPEED_LIMIT_UP=100
        logging:
            driver: json-file
            options:
                max-size: 10m
        ports:
            - 9091:9091
        image: haugene/transmission-openvpn
        restart: unless-stopped