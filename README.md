# Temelden Zirveye Flutter Derslerinde Aldığım Notlar
### Flutter ve Dartı az biliyorum ayrıntılara , kullanmadığım özelliklere ve detaylara da dikkat edeyim derken kendim ve böyle düşünenler için aldığım notlar.
--Not: Bazı kodlarda hata olabilir orda aktarmak istenene odaklanın, doğru kullanımı zaten bulabilirsiniz.

- Eğer Row ya da Col kısaysa ``.extended `` kullanabilirsin. daire sekli yerine stadium  sekli olur.
ornek:
```dart
 FloatingActionButton.extended(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child:Row(
          mainAxisSize: MainAxisSize.min,
          children: <Widget>[
            Icon(Icons.add),
            SizedBox(width: 5,),
            Text('Increment'),
          ],
        ),
      )
```
- ThemeData.dark() kullanarak dark modu aktif edebilirsin.
- Style classi oluşturman kodun okunurluğunu arttırır.
ornek:

```dart
class Style {
  static const TextStyle title = TextStyle(
    fontSize: 20,
    fontWeight: FontWeight.bold,
  );
}
```
- Stringleri birleştirmek için $ kullanabilirsin.
ornek:

```dart
Text('Your name is $name and length is ${name.length}'),
```


- Style classi kullanmanı gerektirmeyen bir diğer özellikse default temalardır. Belirli özelliklerini ``copyWith`` ile değiştirebilirsin.

ornek:

```dart
ThemeData(
   Theme.of(context).textTheme.headline4.copyWith(
     color: Colors.red,
   ),
```
 - asagidaki koda dikkat
 ornek:
```dart
final String? name = 'Flutter Demo Home Page';
Text(name!) // Yanlıs Kullanım!!! 
Text(name ?? '') // Dogru Kullanım
  ```

- Stil sınıfları oluştururken de mesela olusturdugumuz renk sınıflarından yaralanabiliriz.
ornek:
```dart
class ProjectStyle {
  static const TextStyle title = TextStyle(
    fontSize: 20,
    fontWeight: FontWeight.bold,
    color: ProjectColor.welcomeColor,
  );
}
class ProjectColor {
  static const Color welcomeColor = Color(0xffFF0000);
}
```

- Dosyadaki string ifadeleri de bir classta toplayabilirsin.
ornek:
```dart
widget {
    final ProjectKeys keys = ProjectKeys();
    return  Text(keys.welcome);
    );
}
class ProjectKeys {
  final String welcome = 'Welcome';
}
```
- Material app içindeki ``title`` uygulamayı diğer uygulamalarla goruntulerken gozuken ismidir.
- Material app projede bir tane olmalıdır. Aksi durumda routing bozulur vs.
- Container içindeki ``constraint`` kullanımı 
ornek:
```dart
Container(
  constraints: BoxConstraints(
    maxWidth: 200,
    maxHeight: 200,
  ),
  child: Text('Hello World'),
)
```
- ``padding`` içerden uzaklık ``margin`` dıştan uzaklık
- Birden fazla kullanılacak decoration için bir class oluşturabilirsin.
ornek:
```dart
// ornek - 1
class ProjectConainterDecoration extends BoxDecoration {
  ProjectConainterDecoration()
      : super(
          color: Colors.white,
    borderRadius: BorderRadius.all(Radius.circular(10)),
    boxShadow: [
      BoxShadow(
        color: Colors.black12,
        blurRadius: 10,
        spreadRadius: 5,
      ),
    ],
        );
}
// ornek - 2
class ProjectUtility {
    static BoxDecoration boxDecoration=BoxDecoration(
             color: Colors.white,
    borderRadius: BorderRadius.all(Radius.circular(10)),
    boxShadow: [
      BoxShadow(
        color: Colors.black12,
        blurRadius: 10,
        spreadRadius: 5,
      ),
    ],);
        
}
```
- scaffold 3 ana widgeti barındırır.
  - appbar
  - body
  - bottomNavigationBar

- ``FloatingAcionButon`` centerde hoş duruyo
- ``bottomsheet`` asagidan yukarı doğru açılan bir pencere , extendbody 
- ``bottomnavbarlara`` da üstteki classlardaki stylelar aktarılabilir.
- buton türleri  bunların onpressini null yaparsan buton aktif olmaz. enable olayı gibi . Text butonda renk degistirme yerine outlineda daha kolay
-butonların sonuna `.icon` konarak iconlu butonlar oluşturulabilir.
  - textbutton
  - elevatedbutton
  - floatingactionbutton
  - iconbutton
  - outlinebutton
  - togglebutton
  - inkwell
    Borders
    - RoundedRectangleBorder
    - CircleBorder
- appbarda ``leading`` uctaki icon, ``actions`` sondaki sey ,``centertitle`` onemli, bg kaldırma icin transparent yap ve elevation 0 yap,``systemoverlaystyle`` ile statusbar rengini değiştir(statusbar appbarın da üstü olan kısım appbar ile status renkleri aynı olmalı)) ,
- ``automaticallyImplyLeading``: false yaparsan appbardaki geri butonu kaldırılır.
- projedeki her appbar için aynı olan özellikleri mainde ``themedataya`` ``copywith`` ile ekleyebilirsin.Copywith parenttan alır eğer iletirse kendi özelliklerini ekler childa salar.
- parametreler arasından {} içindekiler harici rqeuired olanlar.
-``outlinebuttnları`` kullanmayı unutma diğer hallerine kıyasla daha iyi
- renkleri isimlendirmek için https://chir.ag/projects/name-that-color/ kullanabilirsin.
- static yaparken dikkatli ol dedi,
- eğer renk verirken temadan alırsan tema değişiminde ona uygun bir renk değişimi olur yorulmazsın.
- hani color: Colors.red yaparken ``enumaration`` kullanılıyo kendi renklerini de oluşturabilirsin.
- kodların classları birbirinden ayrı olsun , oop kullanıyoruz o kadar.
ornek:
```dart
//static ornek olması için normalde static kullanmayız
widget {
    color:ColorsItems.porchase,
}
class ColorsItems {
  static const Color porchase = Color(0xffEDBF61);
  static const Color sulu = Color.fromRGBO(198, 237, 97, 1);
}
```


-eger sadece o file üzerinden erişilecekse file private yap _ ile başlat
```dart	
// wigeta atamak için required vs hallediyoz
final String text2 = "veli";
 widget { _TitleTextWidget(text: text2),
           _TitleTextWidget(text: "veli2"),
          }
        
class _TitleTextWidget extends StatelessWidget {
  const TitleTextWidget({Key? key, required this.text}) : super(key: key);
  final String text;

  @override
  Widget build(BuildContext context) {
    return Text(
      text,
      style: Theme.of(context).textTheme.headline3,
    );
  }
}
```
-widgetlar iki yandan da eşit uzaklıkta olmalı , paddingi kullanman işiine yararr , symetric veritcal ve horizontal kullan,
   - eğer aynı alanda her componente aynı paddingi ekliyorsan yanlış yapıyorsun. Onun yerine o özelliği parentine ver.
ornek:
```dart
//standardı sağlamak için boyle yapanzi
widget {
    ...
     padding: ProjectPadding.pagePaddingVertical,
     ...
}
class ProjectPadding {
  static const pagePaddingVertical = EdgeInsets.symmetric(vertical: 10);

  static const pagePaddingRightOnly = EdgeInsets.only(right: 20);
}
```
- Card Borderları
  - RoundedRectangleBorder
  - CircleBorder
  - StadiumBorder

Custom Card oustururken içinde child olmasını engellemek için childi asagidaki gibi yaparak kullanabiliriz
- Ayrıca yine mainde ``cardTheme`` ile cardlar için genel bir tema oluşturabiliriz.
ornek:
```dart
//burada keyin dışında required child eklenir. final widget child a atanır ordan da widgeta gönderilir.
widget {
 children: [
    _CustomCard(
              child: const SizedBox(
            height: 100,
            width: 300,
            child: Center(child: Text('Ali')),
          )),
 ]
}

class _CustomCard extends StatelessWidget {
  _CustomCard({Key? key, required this.child}) : super(key: key);//<<<
  final Widget child;//<<<
  final roundedRectangleBorder = RoundedRectangleBorder(borderRadius: BorderRadius.circular(20));

  @override
  Widget build(BuildContext context) {
    return Card(
      margin: ProjectMargins.cardMargin,
      child: child,//<<
    );
  }
}
```
- assette neler tutuyoruz
    - resimler
    - fontlar
    - jsonlar
    - iconlar
    - diller
    - config dosyaları
- Image eklerken ``Image.network`` olanında ``errorBuilder`` kullanıp placeholder ekleyebiliriz.
ornek:
```dart
errorBuilder: (context, error, stackTrace) => const Icon(Icons.abc_outlined),
```
- Text() içindeki metne sağ tıklayıp ``extract local variable`` yapıp ayırabiliriz.Onu da yukarı at. karmaşık gözükmesin.







