# Gerekli kütüphaneleri projeye ekliyoruz.
import discord  # Discord ile çalışmamızı sağlayan ana kütüphane.
from discord.ext import commands  # Botumuza komutlar eklememizi kolaylaştıran bir sistem.

# Botun mesajları görmesi ve onlara tepki vermesi için izin ayarları yapıyoruz.
intents = discord.Intents.default()  # Varsayılan izin ayarlarını alıyoruz.
intents.message_content = True  # Botun mesaj içeriklerini görmesine izin veriyoruz.

# Botumuzu başlatıyoruz.
bot = commands.Bot(command_prefix='$', intents=intents)
# $ işareti, komutlarımızın başına yazmamız gereken özel bir işarettir.
# Örneğin, bir komut çağırmak için "$hello" yazmamız gerekir..

# Bot Discord'a bağlandığında çalışacak bir kod yazıyoruz.
@bot.event  # Bu, belirli olaylar olduğunda çalışan kod parçalarını belirtmek için kullanılır.
async def on_ready():  # Bot Discord'a başarıyla bağlandığında çalışacak olan kod.
    print(f'{bot.user} olarak giriş yaptık')  # Konsolda, bot

# Bot için bir komut ekliyoruz.
@bot.command()  # Botun anlayacağı bir komut oluşturuyoruz.
async def hello(ctx):  # "hello" adında bir komut. Kullanıcı "$hello" yazdığında bu çalışır.
    await ctx.send(f'Merhaba {bot.user}! Ben bir botum!')
    # Kullanıcının yazdığı yere (sohbet ekranına) mesaj gönderir:
    # "Merhaba [botun adı]! Ben bir botum!"

# Başka bir komut ekliyoruz: Bu komut, bir kişinin Discord sunucusuna ne zaman katıldığını gösterir.
@bot.command()  # Bot için yeni bir komut oluşturuyoruz.
async def joined(ctx, member: discord.Member):  
    """Bir kişinin sunucuya ne zaman katıldığını söyler."""
    # Kullanıcı "$joined @kisiadi" yazarsa, bu komut çalışır.
    await ctx.send(f'{member.name} joined {discord.utils.format_dt(member.joined_at)}')
    # Örneğin: "Ahmet joined 5 Aralık 2024"

@bot.command()
async def cevre(ctx):
    await ctx.send(
        "🌍 Çevre kirliliğini azaltmak için geri dönüşüm yapmalı, "
        "çöpleri yere atmamalı, suyu tasarruflu kullanmalı ve doğayı korumalıyız."
    )

@bot.command()
async def esyalar(ctx):
    await ctx.send(
        "🌱 Çevre dostu eşyalar:\n"
        "🛍️ Bez çanta\n"
        "🥤 Yeniden kullanılabilir matara\n"
        "🔋 Şarj edilebilir pil\n"
        "💡 LED ampul\n"
        "🚲 Bisiklet"
    )

@bot.command()
async def bilgi(ctx):
    await ctx.send(
        "🌍 Çevre kirliliği, insanların doğaya bıraktığı atıklar nedeniyle oluşur. "
        "Hava, su ve toprak kirliliği canlıların yaşamını olumsuz etkiler. "
        "Bu nedenle geri dönüşüm yapmak ve çevreyi temiz tutmak çok önemlidir."
    )

@bot.command()
async def lityumpil(ctx):
    await ctx.send(
        "🔋 Lityum piller telefonlarda, bilgisayarlarda ve elektrikli araçlarda kullanılır. "
        "Normal çöpe atılmamalıdır. Geri dönüşüm kutularına veya pil toplama noktalarına bırakılmalıdır."
    )

quiz_sorular = {
    1: {
        "soru": "❓ Kullanılmış piller nereye atılmalıdır?\nA) Normal çöp\nB) Pil toplama kutusu",
        "cevap": "B"
    },
    2: {
        "soru": "❓ Hangisi çevre dostudur?\nA) Bez çanta\nB) Plastik poşet",
        "cevap": "A"
    },
    3: {
        "soru": "❓ Hava kirliliğini artıran nedir?\nA) Araç egzozları\nB) Ağaçlar",
        "cevap": "A"
    },
    4: {
        "soru": "❓ Hangisi geri dönüştürülebilir?\nA) Kağıt\nB) Pilav",
        "cevap": "A"
    }
}

@bot.command()
async def quiz(ctx):
    global aktif_soru
    aktif_soru = 1
    await ctx.send(
        "📚 Çevre Kirliliği Quizine Hoş Geldin!\n\n"
        + quiz_sorular[1]["soru"]
    )

@bot.command()
async def cevap(ctx, secim):
    global aktif_soru

    if secim.upper() == quiz_sorular[aktif_soru]["cevap"]:
        await ctx.send("✅ Doğru! Sonraki soru için $devam yaz.")
    else:
        await ctx.send(
            f"❌ Yanlış! Doğru cevap: {quiz_sorular[aktif_soru]['cevap']}\n"
            "Sonraki soru için $devam yaz."
        )

@bot.command()
async def devam(ctx):
    global aktif_soru

    aktif_soru += 1

    if aktif_soru in quiz_sorular:
        await ctx.send(quiz_sorular[aktif_soru]["soru"])
    else:
        await ctx.send("🏆 Tebrikler! Çevre Quizini tamamladınız.")


bot.run("token")
