{
    "log": {
        "access": "",
        "error": "",
        "loglevel": ""
    },
    "inbound": {
        "port": 1080,
        "listen": "0.0.0.0",
        "protocol": "socks",
        "settings": {
            "auth": "noauth",
            "udp": true,
            "ip": "127.0.0.1",
            "clients": null
        },
        "streamSettings": null
    },
    "outbound": {
        "tag": "agentout",
        "protocol": "vmess",
        "settings": {
            "vnext": [{
                    "address": "service-1",
                    "port": 443,
                    "users": [{
                        "id": "passwd",
                        "alterId": 32,
                        "security": "aes-128-gcm"
                    }]
                },
                {
                    "address": "service-2",
                    "port": 443,
                    "users": [{
                        "id": "passwd",
                        "alterId": 32
                    }]
                },
                {
                    "address": "service-3",
                    "port": 443,
                    "users": [{
                        "id": "passwd",
                        "alterId": 32
                    }]
                }
                // 如果还有更多服务器可继续添加
            ]
        },
        "streamSettings": {
            "network": "kcp",
            "security": "",
            "tcpSettings": null,
            "kcpSettings": {
                "mtu": 1350,
                "tti": 50,
                "uplinkCapacity": 12,
                "downlinkCapacity": 100,
                "congestion": false,
                "readBufferSize": 2,
                "writeBufferSize": 2,
                "header": {
                    "type": "wechat-video",
                    "request": null,
                    "response": null
                }
            },
            "wsSettings": null
        },
        "mux": {
            "enabled": true
        }
    },
    "inboundDetour": null,
    "outboundDetour": [{
            "protocol": "freedom",
            "settings": {
                "response": null
            },
            "tag": "direct"
        },
        {
            "protocol": "blackhole",
            "settings": {
                "response": {
                    "type": "http"
                }
            },
            "tag": "blockout"
        }
    ],
    "dns": {
        "servers": [
            "8.8.8.8",
            "8.8.4.4",
            "localhost"
        ]
    },
    "routing": {
        "strategy": "rules",
        "settings": {
            "domainStrategy": "IPIfNonMatch",
            "rules": [{
                    "type": "field",
                    "port": null,
                    "outboundTag": "direct",
                    "ip": [
                        "0.0.0.0/8",
                        "10.0.0.0/8",
                        "100.64.0.0/10",
                        "127.0.0.0/8",
                        "169.254.0.0/16",
                        "172.16.0.0/12",
                        "192.0.0.0/24",
                        "192.0.2.0/24",
                        "192.168.0.0/16",
                        "198.18.0.0/15",
                        "198.51.100.0/24",
                        "203.0.113.0/24",
                        "::1/128",
                        "fc00::/7",
                        "fe80::/10"
                    ],
                    "domain": null
                },
                {
                    "type": "field",
                    "port": null,
                    "outboundTag": "agentout",
                    "ip": null,
                    "domain": [
                        "ip111.cn"
                    ]
                },
                {
                    "type": "chinasites",
                    "port": null,
                    "outboundTag": "direct",
                    "ip": null,
                    "domain": null
                },
                {
                    "type": "chinaip",
                    "port": null,
                    "outboundTag": "direct",
                    "ip": null,
                    "domain": null
                }
            ]
        }
    }
}# v2ray-config
