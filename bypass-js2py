import re,requests,js2py#pip install js2py
import json,time
#jschl-answer icin gerekli kodlarin regexi
regexddos = r"(var s.+)\n.+\n.+\n.+\n.+\n.+\n.+\n........(.+)"
#formdaki get(?) istegi icin malzemeler
regexform = r"jschl_vc\".value=\"(.+)\"\/>\n.+value=\"(.+)\""

from random import choice

#Random UserAgent
agent= ['Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.99 Safari/537.36',
'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.99 Safari/537.36',
'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.99 Safari/537.36',
'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_1) AppleWebKit/602.2.14 (KHTML, like Gecko) Version/10.0.1 Safari/602.2.14',
'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.71 Safari/537.36',
'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.98 Safari/537.36',
'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.98 Safari/537.36',
'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.71 Safari/537.36',
'Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.99 Safari/537.36',
'Mozilla/5.0 (Windows NT 10.0; WOW64; rv:50.0) Gecko/20100101 Firefox/50.0'
'Mozilla/5.0 (iPhone; CPU iPhone OS 10_3_1 like Mac OS X) AppleWebKit/603.1.30 (KHTML, like Gecko) Version/10.0 Mobile/14E304 Safari/602.1',
'Mozilla/5.0 (Linux; U; Android 4.4.2; en-us; SCH-I535 Build/KOT49H) AppleWebKit/534.30 (KHTML, like Gecko) Version/4.0 Mobile Safari/534.30',
'Mozilla/5.0 (Linux; Android 7.0; SM-G930V Build/NRD90M) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.125 Mobile Safari/537.36',
'Mozilla/5.0 (Linux; Android 7.0; SM-A310F Build/NRD90M) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.91 Mobile Safari/537.36 OPR/42.7.2246.114996'
'Opera/9.80 (J2ME/MIDP; Opera Mini/5.1.21214/28.2725; U; ru) Presto/2.8.119 Version/11.10',
'Mozilla/5.0 (Android 7.0; Mobile; rv:54.0) Gecko/54.0 Firefox/54.0',
'Mozilla/5.0 (Linux; U; Android 7.0; en-US; SM-G935F Build/NRD90M) AppleWebKit/534.30 (KHTML, like Gecko) Version/4.0 UCBrowser/11.3.8.976 U3/0.8.0 Mobile Safari/534.30',
'Mozilla/5.0 (Linux; Android 7.0; SAMSUNG SM-G955U Build/NRD90M) AppleWebKit/537.36 (KHTML, like Gecko) SamsungBrowser/5.4 Chrome/51.0.2704.106 Mobile Safari/537.36',
'Mozilla/5.0 (Linux; U; Android 7.0; en-us; MI 5 Build/NRD90M) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/53.0.2785.146 Mobile Safari/537.36 XiaoMi/MiuiBrowser/9.0.3',
'Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; Microsoft; Lumia 950)',
'Mozilla/5.0 (Windows Phone 10.0; Android 6.0.1; Microsoft; Lumia 950) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/52.0.2743.116 Mobile Safari/537.36 Edge/15.14977',
'Mozilla/5.0 (Windows Phone 10.0; Android 6.0.1; Microsoft; Lumia 950) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/52.0.2743.116 Mobile Safari/537.36 Edge/15.14977',
'Mozilla/5.0 (Linux; Android 6.0.1; SM-G920V Build/MMB29K) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/52.0.2743.98 Mobile Safari/537.36']
 

ua=choice(agent)
headers = {
    'user-agent': ua,
    'accept': "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8",
    'accept-encoding': "gzip, deflate",
    'accept-language': "tr-TR,tr;q=0.9,en-US;q=0.8,en;q=0.7",
    'connection': "close"
    }
import pickle
def save_cookies(requests_cookiejar, filename):
    with open(filename, 'wb') as f:
        pickle.dump(requests_cookiejar, f)

def load_cookies(filename):
    with open(filename, 'rb') as f:
        return pickle.load(f)

def get(url):
    a=requests.get(url)
    return a.text


proxyApi="https://pubproxy.com/api/proxy?https=true&cookies=true&user_agent=true&format=json"
diziProxy=json.loads(get(proxyApi))
p=diziProxy["data"][0]["ipPort"]
c=diziProxy["data"][0]["country"]
print c+"\t"+p
http_proxy  = "http://"+p
https_proxy = "https://"+p
proxyDict = { 
    "http"  : http_proxy, 
    "https" : https_proxy
}

def sayfa_ac(link):
    page = requests.get(link,headers=headers,proxies=proxyDict)
    return page.text


def jsruncookie(link):
    slen=link.replace('https://','').replace('http://','')
    print slen
    #ua="Mozilla/5.0 (Linux; Android 7.0; SM-G930V Build/NRD90M) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.125 Mobile Safari/537.36"
    
    headers = {
    'user-agent': ua,
    'referer':link,
    'accept': "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8",
    'accept-encoding': "gzip, deflate",
    'accept-language': "tr-TR,tr;q=0.9,en-US;q=0.8,en;q=0.7",
    'connection': "close"
    }
    p=open(slen+"ip.txt", 'rb')
    p=p.read()
    http_proxy  = "http://"+p
    https_proxy = "https://"+p
    proxyDict = { 
        "http"  : http_proxy, 
        "https" : https_proxy
    }
    
    page = requests.get(link,headers=headers,proxies=proxyDict,cookies=load_cookies(slen))
    return page.text

def jsrun(site):
    slen=site.replace('https://','').replace('http://','')
    title=slen
    slen=str(len(slen))+";"#11 https://example.com --> 'example.com'.length >> 11
    print slen
    source=sayfa_ac(site)
    if(source.find('DDoS')>-1):
        print "cloudflare ok."
        jstext=re.findall(regexddos,source)
        fr=re.findall(regexform,source)
        f=fr[0]
        #print f[0]#jschl_vc
        #print f[1]#pass
        t=jstext[0]
        js1=t[0]
        js2=t[1]
        #js2py icin bazi degisiklikler..
        js2=js2.replace("a.value","a").replace("t.length;","15;").replace("'; 121'","return a;")
        #print js1
        #print js2
        jscrpt=js2py.eval_js("function jscrpt(){"+js1+js2+"}")
        url=str(site)+"/cdn-cgi/l/chk_jschl?jschl_vc="+str(f[0])+"&pass="+str(f[1])+"&jschl_answer="+str(jscrpt())
        s = requests.Session()
        r=s.get(url,headers=headers,proxies=proxyDict)
        #print r.text
        print s.cookies.get_dict()#set edilen cerezler
        cerez=str(s.cookies.get_dict())
        if(cerez.find('cf_clearance')>-1):
            save_cookies(s.cookies, title)
            print "saved cookies"
            file=open(title+"-ip.txt","wb")
            file.write(p)
            print "saved ip address"
            file=open(title+"-ua.txt","wb")
            file.write(ua)
        print headers
        e=s.get(site,headers=headers,proxies=proxyDict)
        kaynak=e.text#gercek sayfamizin kaynak kodlari
        #print kaynak
        if(kaynak.find('DDoS')>-1):
            print "no set cookies"
            print "change ip address"
            #jsrun(site)
        else:
            print "bypass cloudflare ok!"
            #print kaynak


print jsrun("https://blabla")#cloudflare cf bypass site

