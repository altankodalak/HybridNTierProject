Identity => Sizin icin hazýr yetkilendirme ve rol sisteminin veritabanýna Microsoft tarafýndan dahil edilmesidir

Entities
************
*Microsoft.AspNetCore.Identity => Identity iþlemleri icin indirdigimiz bir kütüphanedir...BUrada dikkat edin Core olmayan bir Identity Package'ini referans almamalýsýnýz...(Identity iþlemleri icin kastettigimiz kullanýcý ekleme, login olma, signin olma , sifremi unuttum, mail gönderme)


*Microsoft.Extensions.Identity.Stores => NetCore MVC'den ve EF'ten bagýmsýz bir katmanda COre Identity yapýsý kullanýlacaksa Identity kütüphanesinin yanýnda Stores kütüphanesinin de indirilmesi gereklidir...

--------------------------------
MAP(Entities katmanýndan referans alýr)
********
*Microsoft.EntityFrameworkCore => EF iþlemlerinin temeli bu kütüphaneden baslar...(IEntityTypeConfiguration Interface'i de bu kütüphanededir...)
*Microsoft.EntityFrameworkCore.SqlServer => Core'da IEntityTypeConfiguration'in Sql server teknolojisi icin kullanýlmasýný saglayan ve implement edilmiþ metotlarý bulunduran kütüphanedir (HasColumnName,HasColumnType)

-------------------------------------

DAL(MAP'ten referans alýr dolayýsýyla zincirleme olarak Core platfromunda Map'in icindeki ENTITIES de gelecegi icin ENTITIES'ten referans almak zorunda kalmayacagýz)

*Microsoft.EntityFrameworkCore => Ýhtiyacý vardýr ama zaten Map'ten gelmektedir...
*Microsoft.EntityFrameworkCore.SqlServer => Ýhtiyacý vardýr ama Map'ten gelmektedir...
*Microsoft.EntityFrameworkCore.Tools => Migration iþlemlerini terminalden yapmak icin Tools kütüphanesine ihtiyacý vardýr...
*Microsoft.EntityFrameworkCore.Proxies => LazyLoading iþlemlerinin acýlabilmesi icin
*Microsoft.AspNetCore.Identity.EntityFrameworkCore => Sizin Context sýnýfýnýz eger siz Identity kullanýyorsanýz eskisi gibi DbContext'ten miras alamaz... Burada miras almanýz gerkeen sýnýf IdentityDbContext class'ýndan miras almalýdýr...O class da bu kütüphanededir...

---------------------------------------------

COMMON

**********

SessionExtension sýnýfý icin... Dikkat edin artýk burada farklý bir katmanda ve .Net Standart Class Library'sindesiniz...O yüzden normal þartlardaki gibi SessionExtension icin kütüphaneler otomatik gelmez...

*Microsoft.AspNetCore.HTTP.Features => ISession tipini kullanmanýzý saglar
*Microsoft.AspNetCore.HTTP.Extensions => Common katmanýnda ISession tipinin kullanmak istedigimiz GetString ve SetString gibi extension metotlarýna ulasabilmenizi saglar...
*Newtonsoft.JSON => JSON Serialize ve Deserialize iþlemleri icin indirdigimiz kütüphanedir...

------------------------------
BLL(DAL'den referans alýr)
**************
*Microsoft.EntityFrameworkCore => Ýhtiyacý vardýr ama zaten DAL'den gelmektedir...Service Injection options ayarlarý yapýlacaktýr...
*Microsoft.EntityFrameworkCore.SqlServer => Ýhtiyacý vardýr ama zaten DAL'den gelmektedir...Service INjection yapýlýrken Options'un UseSqlServer metodunu kullanmasý gerekir o yüzden ihtiyacý vardýr...
*Microsoft.AspNetCore.Identity => Ýhtiyacý vardýr ama zincirleme referans olarak gelir...Identity servicelerini inject etmek icin (Dependency Injection'a bildirmek icin ihtiyacý vardýr)
*System.Configuration.ConfigurationManager => Mevcut calýsan projenin configuration'inina baska katmanlardan ulasabilmek icin indirmeni gereken küütüphanedir...


------------------------


UI(BLL'den) --Email vs sýnýflarýnýz varsa oradan referans almak zorunda olacaktýr
**********
*Microsoft.EntityFrameworkCore(chain reference olarak gelir)
*Microsoft.EntityFrameworkCore.SqlServer(chain reference olarak gelir)
*Microsoft.EntityFrameworkCore.Design => Migration icin Tools kütüphanesini DAL'den ekleyerek ayrý bir katmanda terminal iþlemleri yaptýgýmýzdan dolayý o Tools'a destek verebilmesi icin UI'a bu Design kütüphanesinin indirilmesi gerekir...