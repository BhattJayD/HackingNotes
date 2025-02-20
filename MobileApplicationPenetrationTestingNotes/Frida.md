#### Install Frida

Ref : https://frida.re/docs/quickstart/

```bash
python3 -m venv venv
```

```bash
source venv/bin/activate
```

```bash
pip install frida-tools
```

#### Download Frida server and push to android

##### Download

```bash
wget https://github.com/frida/frida/releases/download/16.6.6/frida-server-16.6.6-android-x86.xz
```

##### Extract

```bash
tar --xz -xvf frida-server-16.6.6-android-x86.xz
```

##### Push to android

```bash
adb push frida-server-16.6.6-android-x86 /data/local/tmp
```

##### Start server

```bash
adb shell
```

##### Give execution permission

```bash
cd /data/local/tmp; chmod +x frida-server-16.6.6-android-x86
```

##### Run Server

```bash
./frida-server-16.6.6-android-x86
```
