# OpenIPC Wiki
[Mục lục](../README.md)

TP-Link Tapo C110
---

### GPIO
IRLed | WhiteLed | RedLed | GreenLed | Loa | Đặt lại | IRCut
-|-|-|-|-|-|-
GPIO14 | GPIO15 | GPIO46 | GPIO47 | GPIO61 | GPIO66 | GPIO78

```
cli -s .nightMode.irCutPin1 78
cli -s .nightMode.backlightPin 14
cli -s .audio.speakerPin 61
```

---

### Không dây
```
fw_setenv wlandev ssw101b-ssc333-tapo-c110
fw_setenv wlanssid Router
fw_setenv wlanpass 12345678
```


