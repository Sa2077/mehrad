{  
"route": {
    "geoip": {
      "path": "geo-assets\\sagernet-sing-geoip-geoip.db"
    },
    "geosite": {
      "path": "geo-assets\\sagernet-sing-geosite-geosite.db"
    },
    "rules": [
      {
        "inbound": "dns-in",
        "outbound": "dns-out"
      },
      {
        "port": 53,
        "outbound": "dns-out"
      },
      {
        "clash_mode": "Direct",
        "outbound": "direct"
      },
      {
        "clash_mode": "Global",
        "outbound": "select"
      }
    ],
    "auto_detect_interface": true,
    "override_android_vpn": true
  },
  "outbounds": [
    {
      "type": "selector",
      "tag": "select",
      "outbounds": [
        "auto",
        "IP->Iran, Yotube:MisaHiro",
        "IP->Main, Yotube:MisaHiro"
      ],
      "default": "auto"
    },
    {
      "type": "urltest",
      "tag": "auto",
      "outbounds": [
        "IP->Iran, Yotube:MisaHiro",
        "IP->Main, Yotube:MisaHiro"
      ],
      "url": "http://cp.cloudflare.com/",
      "interval": "10m0s"
    },
    {
      "type": "wireguard",
      "tag": "IP->Iran, Yotube:MisaHiro",
      "local_address": [
        "172.16.0.2/32",
        "2606:4700:110:8ca7:fd7e:12c8:ddd1:d080/128"
      ],
      "private_key": "kEKSj4XtY9bsc5cKJlluo9cHphGMGr3wNEDdW2o50H0=",
      "server": "188.114.96.195",
      "server_port": 968,
      "peer_public_key": "bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=
",
      "reserved": "AAAA",
      "mtu": 1280,
      "fake_packets": "5-10"
    },
    {
      "type": "wireguard",
      "tag": "IP->Main, Yotube:MisaHiro",
      "detour": "IP->Iran, Yotube:MisaHiro",
      "local_address": [
        "172.16.0.2/32",
        "2606:4700:110:8ca7:fd7e:12c8:ddd1:d080/128"
      ],
      "private_key": "kEKSj4XtY9bsc5cKJlluo9cHphGMGr3wNEDdW2o50H0=",
      "server": "188.114.96.195",
      "server_port": 968,
      "peer_public_key": "bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=
",
      "reserved": "AAAA",
      "mtu": 1280,
      "fake_packets": "5-10"
    },
    {
      "type": "dns",
      "tag": "dns-out"
    },
    {
      "type": "direct",
      "tag": "direct"
    },
    {
      "type": "direct",
      "tag": "bypass"
    },
    {
      "type": "block",
      "tag": "block"
    }
  ]  
}
