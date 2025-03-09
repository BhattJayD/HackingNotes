### Find Path One liner

The command:
```bash
adb shell "pm path "$(adb shell "pm list packages | grep google" | awk -F: '{print $2}')
```

**In short:**

1. **List Packages:** Finds all installed packages containing "google":

```bash
adb shell "pm list packages | grep google"
```

2. **Extract Package Name:** Extracts only the package name from the output:

```bash
| awk -F: '{print $2}'
```

3. **Get APK Path:** Retrieves the file path of the APK for the first matching package:

```bash
adb shell "pm path <package_name>"
```

4. **Combining It All:** Automatically passes the package name to `pm path` to get the APK path in one command.