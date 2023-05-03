version: '2.1'
services:
  prowlarr:
  ## used for linking web based indices to apps below
    image: lscr.io/linuxserver/prowlarr:latest
    container_name: prowlarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/New_York
    volumes:
      - /home/docker/torrentdata/prowlarr:/config
    ports:
      - 9696:9696
    restart: unless-stopped

  sonarr:
  ## used for TV shows
    image: lscr.io/linuxserver/sonarr:latest
    container_name: sonarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/New_York
    volumes:
      - /home/docker/torrentdata/sonarr:/config
      - /mnt/blackmedia/Videos/Series:/tv #optional
      - /mnt/blackmedia/Torrent:/downloads #optional
      - /mnt/blackmedia/Torrent:/data #optional
    ports:
      - 8989:8989
    restart: unless-stopped

  radarr:
  ## used for movies
    image: lscr.io/linuxserver/radarr:latest
    container_name: radarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/New_York
    volumes:
      - /home/docker/torrentdata/radarr:/config
      - /mnt/blackmedia/Videos/Movies:/movies #optional
      - /mnt/blackmedia/Torrent:/downloads #optional
      - /mnt/blackmedia/Torrent:/data #optional
    ports:
      - 7878:7878
    restart: unless-stopped

  readarr:
  ## used for books
    image: lscr.io/linuxserver/readarr:develop
    container_name: readarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/New_York
    volumes:
      - /home/docker/torrentdata/readarr:/config
      - /mnt/blackmedia/Education/Books:/books #optional
      - /mnt/blackmedia/Torrent:/downloads #optional
    ports:
      - 8787:8787
    restart: unless-stopped
    
  lidarr:
  ## used for music
    image: lscr.io/linuxserver/lidarr:latest
    container_name: lidarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/New_York
    volumes:
      - /home/docker/torrentdata/lidarr:/config
      - /mnt/blackmedia/Music:/music #optional
      - /mnt/blackmedia/Torrent:/downloads #optional
      - /mnt/blackmedia/Torrent:/data #optional
    ports:
      - 8686:8686
    restart: unless-stopped