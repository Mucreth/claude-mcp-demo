# MCP ile Otomatik Tarım Projesi

Bu örnek proje, MCP kullanarak basit bir otomatik tarım sistemi oluşturmayı göstermektedir.

## Proje Tanımı

Bu projede MCP kullanarak şunları yapacağız:
- Belirli bir alanda ekin kontrolü
- Olgun ekinlerin otomatik hasat edilmesi
- Hasat edilen alanların yeniden ekilmesi
- İşlemin belirli aralıklarla tekrarlanması

## Gereksinimler

- MCP'nin kurulu olması
- Düz bir tarım alanı (en az 5x5 blok)
- Komut bloklarını yerleştirebileceğiniz bir alan
- Birkaç tohum (buğday, havuç, patates vb.)

## Kurulum Adımları

### 1. Tarım Alanını Hazırlama

1. Düz bir alanda, 5x5 veya daha büyük bir tarım alanı oluşturun
2. Alanın etrafını işaretlemek için farklı bloklar kullanabilirsiniz
3. Toprağı çapalayın ve su ile nemlendirin

### 2. Komut Bloklarını Yerleştirme

1. Tarım alanınızın yakınında 3 komut bloğu yerleştirin:
   - İlk blok: Ekinleri kontrol edecek
   - İkinci blok: Hasat işlemini gerçekleştirecek
   - Üçüncü blok: Yeniden ekme işlemini yapacak

### 3. MCP Scriptlerini Oluşturma

#### Ekin Kontrol Scripti
```
/mcp script new crop_check

# Belirtilen alanda olgun ekin var mı kontrol et
$ripe_crops = 0
scan area from ~-2 ~0 ~-2 to ~2 ~0 ~2 {
  if block == minecraft:wheat[age=7] 
      || block == minecraft:carrots[age=7] 
      || block == minecraft:potatoes[age=7] {
    $ripe_crops = $ripe_crops + 1
  }
}

# Olgun ekin varsa hasat scriptini çalıştır
if $ripe_crops > 0 {
  /mcp script run harvest_crops
  /title @p actionbar {"text":"Hasat ediliyor...","color":"green"}
} else {
  /title @p actionbar {"text":"Henüz hasat edilecek ekin yok","color":"yellow"}
}

/mcp script save
```

#### Hasat Scripti
```
/mcp script new harvest_crops

# Olgun ekinleri hasat et
scan area from ~-2 ~0 ~-2 to ~2 ~0 ~2 {
  if block == minecraft:wheat[age=7] 
      || block == minecraft:carrots[age=7] 
      || block == minecraft:potatoes[age=7] {
    /setblock $x $y $z air destroy
    # Hasat partikül efekti ekle
    /particle minecraft:happy_villager $x $y $z 0.5 0.5 0.5 0 10
  }
}

# Kısa bir gecikme ver ve yeniden ekme scriptini çalıştır
wait 10t
/mcp script run replant_crops

/mcp script save
```

#### Yeniden Ekme Scripti
```
/mcp script new replant_crops

# Boş tarım alanlarını yeniden ek
scan area from ~-2 ~0 ~-2 to ~2 ~0 ~2 {
  if block == minecraft:farmland && block_above == minecraft:air {
    # Ekin tipini belirle - burada buğday kullanıyoruz
    /setblock $x $($y+1) $z minecraft:wheat[age=0]
    # Ekme partikül efekti ekle
    /particle minecraft:villager_happy $x $($y+1) $z 0.3 0.3 0.3 0 5
  }
}

/title @p actionbar {"text":"Ekinler yeniden ekildi","color":"green"}

/mcp script save
```

#### Otomatik Kontrol Scripti
```
/mcp script new auto_farm

# Bu script, her 5 dakikada bir ekin kontrolü yapar
/title @p title {"text":"Otomatik Tarım","color":"green"}
/title @p subtitle {"text":"Başlatıldı","color":"yellow"}

while true {
  /mcp script run crop_check
  wait 5m
}

/mcp script save
```

## Kullanım

1. Tarım alanınızın ortasında durun
2. Otomatik tarım scriptini başlatmak için şu komutu girin:
   ```
   /mcp script run auto_farm
   ```
3. Scripti durdurmak isterseniz:
   ```
   /mcp script stop auto_farm
   ```

## Özelleştirme

Bu temel scripti kendi ihtiyaçlarınıza göre özelleştirebilirsiniz:

- Tarım alanının boyutunu değiştirmek için `scan area` komutundaki koordinatları ayarlayın
- Farklı ekin tipleri için `if block == ...` kontrollerini güncelleyin
- Kontrol sıklığını değiştirmek için `wait 5m` değerini ayarlayın (s:saniye, m:dakika, h:saat)
- Daha büyük tarlalar için alanı bölümlere ayırarak birden fazla tarama yapabilirsiniz

## Sorun Giderme

### Hiçbir şey hasat edilmiyor
- Koordinatların doğru olduğundan emin olun
- Ekinlerin tam olarak olgunlaştığını kontrol edin
- Hata ayıklama için `/mcp debug on` komutunu kullanın

### Script çalışmıyor
- Tüm scriptlerin doğru şekilde kaydedildiğinden emin olun
- Yazım hatalarını kontrol edin
- MCP'yi `/mcp reload` komutu ile yeniden yükleyin

## İleri Seviye Geliştirmeler

Bu basit örnek üzerine ekleyebileceğiniz bazı ileri seviye özellikler:

- Hasat edilen ürünleri otomatik olarak sandıklarda depolama
- Farklı ekin türleri için ayrı kontroller
- İstatistik toplama (toplam hasat, verimlilik vb.)
- Redstone ile entegrasyon
