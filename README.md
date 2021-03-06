# metadnsq

*dnssrc* - a CoreDNS forwarding/proxy plugin with the main function of triaging based on client sources

This plugin is based on the `github.com/leiless/dnsredir` extension, many thanks to `dnsredir ` for the inspiration


# Example

    . {
        cache 1
        debug
        datahub {
            geoip_path data/geoip.dat
            geosite_path data/geosite.dat
            geoip_cache cn hk jp google apple
            geosite_cache cn hk jp private apple
            geodat_upgrade_url http://xxxx.com
            geodat_upgrade_cron 0 30 0 * * *
            keyword_table cn data/keyword_cn.txt
            reload @every 3s
        }
    
        metadnsq cn {
            max_fails 0
            health_check 30s
            to 114.114.114.114 223.5.5.5
            policy round_robin
        }
    
        metadnsq !cn {
            max_fails 0
            health_check 30s
            to 114.114.114.114 223.5.5.5
            policy round_robin
        }
    }
