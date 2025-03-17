# MCP Temel Komutlar Listesi

Bu belge, Minecraft Command Protocol (MCP) kullanırken ihtiyaç duyacağınız temel komutları içermektedir.

## Genel Komutlar

| Komut | Açıklama | Kullanım Örneği |
|-------|----------|-----------------|
| `/mcp help` | Tüm MCP komutlarını listeler | `/mcp help` |
| `/mcp version` | MCP sürüm bilgisini gösterir | `/mcp version` |
| `/mcp reload` | MCP yapılandırmasını yeniden yükler | `/mcp reload` |
| `/mcp settings` | MCP ayarlarını görüntüler ve düzenler | `/mcp settings render_distance 10` |

## Komut Blokları

| Komut | Açıklama | Kullanım Örneği |
|-------|----------|-----------------|
| `/mcp block create` | Yeni bir komut bloğu oluşturur | `/mcp block create myblock` |
| `/mcp block edit <isim>` | Var olan bir komut bloğunu düzenler | `/mcp block edit myblock` |
| `/mcp block delete <isim>` | Bir komut bloğunu siler | `/mcp block delete myblock` |
| `/mcp block list` | Tüm komut bloklarını listeler | `/mcp block list` |
| `/mcp block copy <kaynak> <hedef>` | Bir komut bloğunu kopyalar | `/mcp block copy myblock mynewblock` |

## Script Komutları

| Komut | Açıklama | Kullanım Örneği |
|-------|----------|-----------------|
| `/mcp script new <isim>` | Yeni bir script oluşturur | `/mcp script new myscript` |
| `/mcp script run <isim>` | Bir scripti çalıştırır | `/mcp script run myscript` |
| `/mcp script stop <isim>` | Çalışan bir scripti durdurur | `/mcp script stop myscript` |
| `/mcp script edit <isim>` | Bir scripti düzenler | `/mcp script edit myscript` |
| `/mcp script list` | Tüm scriptleri listeler | `/mcp script list` |

## Otomasyon Komutları

| Komut | Açıklama | Kullanım Örneği |
|-------|----------|-----------------|
| `/mcp auto start <isim>` | Bir otomasyon sürecini başlatır | `/mcp auto start farm` |
| `/mcp auto stop <isim>` | Bir otomasyon sürecini durdurur | `/mcp auto stop farm` |
| `/mcp auto schedule <isim> <zaman>` | Bir otomasyonu zamanlar | `/mcp auto schedule farm 10m` |
| `/mcp auto repeat <isim> <aralık>` | Yinelenen bir otomasyon ayarlar | `/mcp auto repeat farm 5m` |

## Hata Ayıklama Komutları

| Komut | Açıklama | Kullanım Örneği |
|-------|----------|-----------------|
| `/mcp debug on` | Hata ayıklama modunu açar | `/mcp debug on` |
| `/mcp debug off` | Hata ayıklama modunu kapatır | `/mcp debug off` |
| `/mcp debug log <seviye>` | Günlük kaydı seviyesini ayarlar | `/mcp debug log verbose` |
| `/mcp debug clear` | Hata ayıklama günlüklerini temizler | `/mcp debug clear` |

## Gelişmiş Komutlar

| Komut | Açıklama | Kullanım Örneği |
|-------|----------|-----------------|
| `/mcp export <isim> <dosya>` | Bir yapılandırmayı dışa aktarır | `/mcp export myconfig config.json` |
| `/mcp import <dosya>` | Bir yapılandırmayı içe aktarır | `/mcp import config.json` |
| `/mcp monitor <hedef>` | Bir varlığı veya bloğu izler | `/mcp monitor @e[type=zombie]` |
| `/mcp optimize <hedef>` | Performansı optimize eder | `/mcp optimize scripts` |

## Syntax Örnekleri

### Basit Komut Bloğu Oluşturma
```
/mcp block create myblock
/mcp block edit myblock

# Bloğa komut ekleme
/say Hello World
/give @p diamond 1

# Düzenlemeyi kaydetme
/mcp block save
```

### Koşullu İfade Örneği
```
/mcp script new myscript

# Script içeriği
if entity @p[distance=..5] {
  /say A player is nearby!
  /effect give @p minecraft:regeneration 10 1
} else {
  /say No players around.
}

# Scripti kaydetme
/mcp script save
```

### Döngü Örneği
```
/mcp script new countdown

# Script içeriği
for i = 10, 1, -1 {
  /title @a title {"text":""+i,"color":"gold"}
  /playsound minecraft:block.note_block.harp master @a ~ ~ ~ 1 1
  wait 20t
}
/title @a title {"text":"Go!","color":"green"}
/playsound minecraft:entity.player.levelup master @a ~ ~ ~ 1 0.5

# Scripti kaydetme
/mcp script save
```

## İpuçları

- Çoğu MCP komutu, tab tuşu ile otomatik tamamlama özelliğine sahiptir.
- Düzenleyiciden çıkmak için her zaman komutları kaydetmeyi unutmayın (`/mcp block save` veya `/mcp script save`).
- Hata ayıklama modunu açarak, sorunları daha kolay tespit edebilirsiniz.
- Karmaşık scriptler için, oyun içi düzenleyici yerine harici bir düzenleyici kullanabilir ve `/mcp import` komutu ile içe aktarabilirsiniz.
