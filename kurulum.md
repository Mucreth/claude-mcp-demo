# MCP (Minecraft Command Protocol) Kurulum Rehberi

Bu rehber, MCP'nin Minecraft'a nasıl kurulacağını adım adım açıklamaktadır.

## Gereksinimler

- Minecraft Java Edition (1.16 veya üzeri)
- Forge veya Fabric mod yükleyici
- MCP modunun son sürümü

## Adım Adım Kurulum

### 1. Forge veya Fabric Kurulumu

#### Forge İçin:
1. [Forge web sitesinden](https://files.minecraftforge.net/) Minecraft sürümünüze uygun Forge indirin
2. İndirilen dosyayı çalıştırın ve "Install client" seçeneğini seçin
3. Kurulum tamamlandıktan sonra Minecraft Launcher'ı açın ve profiller listesinden "forge" profilini seçin

#### Fabric İçin:
1. [Fabric web sitesinden](https://fabricmc.net/use/) Fabric Installer'ı indirin
2. İndirilen dosyayı çalıştırın ve Minecraft sürümünüzü seçin
3. "Client" seçeneğinin işaretli olduğundan emin olun ve kurulumu tamamlayın
4. Minecraft Launcher'ı açın ve profiller listesinden "fabric-loader" profilini seçin

### 2. MCP Modunun Yüklenmesi

1. MCP mod dosyasını [resmi web sitesinden](https://mcp.example.com/) veya güvenilir bir mod sitesinden indirin
2. İndirilen `.jar` dosyasını şu konuma kopyalayın:
   - Windows: `%AppData%\.minecraft\mods`
   - macOS: `~/Library/Application Support/minecraft/mods`
   - Linux: `~/.minecraft/mods`
3. Eğer `mods` klasörü yoksa, manuel olarak oluşturun

### 3. Minecraft'ı Başlatma ve Doğrulama

1. Minecraft Launcher'ı açın ve Forge/Fabric profilini seçin
2. Oyunu başlatın ve ana menüye girin
3. "Mods" menüsüne girerek MCP'nin yüklü modlar listesinde görünüp görünmediğini kontrol edin
4. Yeni bir dünya oluşturun veya var olan bir dünyayı açın
5. Sohbet penceresini açarak `/mcp version` komutunu yazın. Eğer mod doğru yüklendiyse, sürüm bilgisini göreceksiniz

## Olası Sorunlar ve Çözümleri

### Mod yüklenmedi
- Mod dosyasının doğru klasörde olduğundan emin olun
- Mod ve Minecraft sürümlerinin uyumlu olduğunu kontrol edin
- Forge/Fabric sürümünün mod için uygun olduğunu doğrulayın

### Çakışma hataları
- Diğer komut bloğu modlarını kaldırın, çünkü MCP ile çakışabilirler
- Minecraft'ı temiz bir profille yeniden başlatmayı deneyin

### Performans sorunları
- MCP ayarlar dosyasında performans optimizasyonları yapabilirsiniz:
  1. `.minecraft/config/mcp.json` dosyasını açın
  2. `performance` bölümündeki değerleri düşürün

## İleri Ayarlar

MCP'nin gelişmiş ayarlarını yapılandırmak için `.minecraft/config/mcp.json` dosyasını düzenleyebilirsiniz. Bu dosya şu bölümleri içerir:

- `commandSettings`: Komutların davranışını özelleştirme
- `blockInteractions`: Blok etkileşimlerini yapılandırma
- `debugging`: Hata ayıklama seçenekleri

## Sonraki Adımlar

Kurulum tamamlandıktan sonra, temel MCP komutlarını öğrenmek için `komutlar.md` dosyasına göz atabilirsiniz.
