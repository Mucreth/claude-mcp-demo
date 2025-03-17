# MCP Hata Ayıklama İpuçları ve Yöntemleri

Bu dokümanda, MCP kullanırken karşılaşabileceğiniz sorunları çözmek için ipuçları ve yöntemler bulacaksınız.

## Temel Hata Ayıklama Adımları

### 1. Hata Ayıklama Modunu Etkinleştirme

MCP hata ayıklama modu, sorunları tespit etmenizde yardımcı olabilecek ek bilgiler sağlar:

```
/mcp debug on
```

Daha ayrıntılı günlük kaydı için:

```
/mcp debug log verbose
```

### 2. Günlük Dosyalarını Kontrol Etme

MCP, `.minecraft/logs/mcp` dizininde günlük dosyaları oluşturur. Bu dosyalarda detaylı hata mesajları bulabilirsiniz:

1. Minecraft'ı kapatın
2. Günlük dosyalarının bulunduğu dizine gidin:
   - Windows: `%AppData%\.minecraft\logs\mcp`
   - macOS: `~/Library/Application Support/minecraft/logs/mcp`
   - Linux: `~/.minecraft/logs/mcp`
3. En son oluşturulan günlük dosyasını açın ve hata mesajlarını inceleyin

### 3. Adım Adım Test Etme

Karmaşık bir MCP scripti hata veriyorsa, adım adım test edin:

1. Scripti küçük parçalara bölün
2. Her parçayı ayrı ayrı çalıştırın
3. Her adımda sonuçları kontrol edin
4. Sorunu bulduğunuzda, o bölümü düzeltin ve tekrar test edin

## Yaygın Sorunlar ve Çözümleri

### Komut Bulunamadı Hatası

**Sorun:** `/mcp` komutları çalışmıyor veya "command not found" hatası alıyorsunuz.

**Çözümler:**
- MCP modunun doğru yüklendiğinden emin olun
- `/reload` komutunu çalıştırın
- Oyunu kapatıp yeniden başlatın
- MCP sürümünün Minecraft sürümünüzle uyumlu olduğunu kontrol edin

### Script Çalışma Hataları

**Sorun:** Script çalıştırıldığında hata veriyor veya beklendiği gibi çalışmıyor.

**Çözümler:**
- Sözdizimi hatalarını kontrol edin (parantezler, noktalı virgüller, vb.)
- Değişken adlarının doğru yazıldığından emin olun
- Koşullu ifadelerdeki mantık hatalarını kontrol edin
- Komutlardaki koordinatların doğru olduğunu doğrulayın

### Performans Sorunları

**Sorun:** MCP scriptleri çalışırken oyun yavaşlıyor.

**Çözümler:**
- Döngülerin optimizasyonunu kontrol edin
- Büyük alanları tarayan scriptleri küçük parçalara bölün
- Zaman gecikmeleri (wait komutları) ekleyin
- `.minecraft/config/mcp.json` dosyasındaki performans ayarlarını düzenleyin

### Bellek Sorunları

**Sorun:** Uzun süre çalışan scriptlerde "out of memory" hatası.

**Çözümler:**
- Minecraft'a daha fazla RAM tahsis edin
- Küresel değişken kullanımını sınırlayın
- Kullanılmayan scriptleri `/mcp script clear <isim>` ile temizleyin
- Çok büyük döngülerde bellek temizleme işlemleri ekleyin

## Gelişmiş Hata Ayıklama Teknikleri

### Debug Mesajları Ekleme

Script içine debug mesajları ekleyerek akışı takip edebilirsiniz:

```
/mcp script new mytest

$counter = 0
for i = 1, 10 {
  $counter = $counter + 1
  /tellraw @p {"text":"Debug: Counter value is now "+$counter,"color":"gray"}
  wait 5t
}

/mcp script save
```

### Değişken Durumunu İzleme

Global değişkenlerin durumunu kontrol etmek için:

```
/mcp vars list
```

Belirli bir değişkenin değerini görüntülemek için:

```
/mcp vars get <değişken_adı>
```

### Performans Profili Oluşturma

Bir scriptin performansını analiz etmek için:

```
/mcp profile start <script_adı>
/mcp script run <script_adı>
/mcp profile end
/mcp profile report
```

### Belirli Blokları Test Etme

Scriptinizde belirli bir bloğun davranışını test etmek için:

```
/mcp test block <x> <y> <z>
```

## İpuçları ve En İyi Uygulamalar

1. **Düzenli Yedekleme:**
   - Karmaşık scriptler üzerinde çalışırken düzenli olarak yedek alın
   - `/mcp export all backups/mybackup.json` komutu ile tüm scriptleri dışa aktarabilirsiniz

2. **Modüler Kod Yazma:**
   - Büyük scriptleri küçük, yeniden kullanılabilir parçalara bölün
   - Her modül tek bir işi yapmalıdır

3. **Hata İşleme:**
   - Kritik bölümlerde try-catch blokları kullanın
   - Olası hataları önceden tahmin edin ve alternatif yollar ekleyin

4. **Belgeleme:**
   - Karmaşık kodları yorum satırları ile belgeleyin
   - Değişkenlerin ve işlevlerin amacını açıklayın

5. **Temiz Kod:**
   - Anlamlı değişken adları kullanın
   - Girintileri düzgün kullanarak kodu okunabilir tutun
   - Kullanılmayan kod parçalarını temizleyin

## Sorun Giderme Kontrol Listesi

Bir sorunla karşılaştığınızda bu adımları izleyin:

1. Hata mesajlarını dikkatlice okuyun
2. Hata ayıklama modunu etkinleştirin
3. Problemi en basit haliyle yeniden oluşturmaya çalışın
4. Günlük dosyalarını kontrol edin
5. Kodu adım adım test edin
6. Forumları ve belgeleri kontrol edin
7. Problemi çözemediyseniz, topluluktan yardım isteyin

## Kaynaklar

- MCP resmi belgeleri
- Minecraft Command Wiki
- MCP Topluluk Forumu
- Minecraft Discord sunucuları
