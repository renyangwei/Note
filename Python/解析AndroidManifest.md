# 解析AndroidManifest

```python
try: 
    import xml.etree.cElementTree as ET 
except ImportError: 
    import xml.etree.ElementTree as ET 

androidNS = 'http://schemas.android.com/apk/res/android'
ET.register_namespace('android', androidNS)

tree = ET.parse(targetManifest)
root = tree.getroot()
# 包名
packageName = root.get('package')
root.set("package", "com.xxx.xxx")
application = root.find("application")
# icon
icon = application.get(getAttribKey("icon"))
application.set(getAttribKey("icon"), "icon")
# appName
appName = application.get(getAttribKey("label"))
# application
applicationClass = application.get(getAttribKey("name"))
# activity
activityNodes = application.findall("activity")
# meta-data
metas = application.findall("meta-data")

def getAttribKey(key):
    return '{' + androidNS + '}' + key
```