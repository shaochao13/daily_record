解压inflate压缩格式：

```java
private static  String unzipString(byte[] zbytes) {

        String str = "";
        ByteArrayInputStream bais = new ByteArrayInputStream(zbytes);
        InflaterInputStream iis = new InflaterInputStream(bais,new Inflater(true));

        ByteArrayOutputStream baos = new ByteArrayOutputStream();

        int c = 0;
        byte[] buf = new byte[512];
        try {
            while (true) {

                c = iis.read(buf);


                if (c == -1)
                    break;

                baos.write(buf, 0, c);
            }

            baos.flush();
            str = baos.toString();
         } catch (IOException e) {
            e.printStackTrace();
        }

        return str;
    }
```


