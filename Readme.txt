Identity => Sizin icin haz�r yetkilendirme ve rol sisteminin veritaban�na Microsoft taraf�ndan dahil edilmesidir

Entities
************
*Microsoft.AspNetCore.Identity => Identity i�lemleri icin indirdigimiz bir k�t�phanedir...BUrada dikkat edin Core olmayan bir Identity Package'ini referans almamal�s�n�z...(Identity i�lemleri icin kastettigimiz kullan�c� ekleme, login olma, signin olma , sifremi unuttum, mail g�nderme)


*Microsoft.Extensions.Identity.Stores => NetCore MVC'den ve EF'ten bag�ms�z bir katmanda COre Identity yap�s� kullan�lacaksa Identity k�t�phanesinin yan�nda Stores k�t�phanesinin de indirilmesi gereklidir...

--------------------------------
MAP(Entities katman�ndan referans al�r)
********
*Microsoft.EntityFrameworkCore => EF i�lemlerinin temeli bu k�t�phaneden baslar...(IEntityTypeConfiguration Interface'i de bu k�t�phanededir...)
*Microsoft.EntityFrameworkCore.SqlServer => Core'da IEntityTypeConfiguration'in Sql server teknolojisi icin kullan�lmas�n� saglayan ve implement edilmi� metotlar� bulunduran k�t�phanedir (HasColumnName,HasColumnType)

-------------------------------------

DAL(MAP'ten referans al�r dolay�s�yla zincirleme olarak Core platfromunda Map'in icindeki ENTITIES de gelecegi icin ENTITIES'ten referans almak zorunda kalmayacag�z)

*Microsoft.EntityFrameworkCore => �htiyac� vard�r ama zaten Map'ten gelmektedir...
*Microsoft.EntityFrameworkCore.SqlServer => �htiyac� vard�r ama Map'ten gelmektedir...
*Microsoft.EntityFrameworkCore.Tools => Migration i�lemlerini terminalden yapmak icin Tools k�t�phanesine ihtiyac� vard�r...
*Microsoft.EntityFrameworkCore.Proxies => LazyLoading i�lemlerinin ac�labilmesi icin
*Microsoft.AspNetCore.Identity.EntityFrameworkCore => Sizin Context s�n�f�n�z eger siz Identity kullan�yorsan�z eskisi gibi DbContext'ten miras alamaz... Burada miras alman�z gerkeen s�n�f IdentityDbContext class'�ndan miras almal�d�r...O class da bu k�t�phanededir...

---------------------------------------------

COMMON

**********

SessionExtension s�n�f� icin... Dikkat edin art�k burada farkl� bir katmanda ve .Net Standart Class Library'sindesiniz...O y�zden normal �artlardaki gibi SessionExtension icin k�t�phaneler otomatik gelmez...

*Microsoft.AspNetCore.HTTP.Features => ISession tipini kullanman�z� saglar
*Microsoft.AspNetCore.HTTP.Extensions => Common katman�nda ISession tipinin kullanmak istedigimiz GetString ve SetString gibi extension metotlar�na ulasabilmenizi saglar...
*Newtonsoft.JSON => JSON Serialize ve Deserialize i�lemleri icin indirdigimiz k�t�phanedir...

------------------------------
BLL(DAL'den referans al�r)
**************
*Microsoft.EntityFrameworkCore => �htiyac� vard�r ama zaten DAL'den gelmektedir...Service Injection options ayarlar� yap�lacakt�r...
*Microsoft.EntityFrameworkCore.SqlServer => �htiyac� vard�r ama zaten DAL'den gelmektedir...Service INjection yap�l�rken Options'un UseSqlServer metodunu kullanmas� gerekir o y�zden ihtiyac� vard�r...
*Microsoft.AspNetCore.Identity => �htiyac� vard�r ama zincirleme referans olarak gelir...Identity servicelerini inject etmek icin (Dependency Injection'a bildirmek icin ihtiyac� vard�r)
*System.Configuration.ConfigurationManager => Mevcut cal�san projenin configuration'inina baska katmanlardan ulasabilmek icin indirmeni gereken k��t�phanedir...


------------------------


UI(BLL'den) --Email vs s�n�flar�n�z varsa oradan referans almak zorunda olacakt�r
**********
*Microsoft.EntityFrameworkCore(chain reference olarak gelir)
*Microsoft.EntityFrameworkCore.SqlServer(chain reference olarak gelir)
*Microsoft.EntityFrameworkCore.Design => Migration icin Tools k�t�phanesini DAL'den ekleyerek ayr� bir katmanda terminal i�lemleri yapt�g�m�zdan dolay� o Tools'a destek verebilmesi icin UI'a bu Design k�t�phanesinin indirilmesi gerekir...