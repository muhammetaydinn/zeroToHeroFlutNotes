# Temelden Zirveye Flutter Derslerinde Aldığım Notlar

### Flutter ve Dartı az biliyorum ayrıntılara , kullanmadığım özelliklere ve detaylara da dikkat edeyim derken kendim ve böyle düşünenler için aldığım notlar.

--Not: Bazı kodlarda hata olabilir orda aktarmak istenene odaklanın, doğru kullanımı zaten bulabilirsiniz.

- Eğer Row ya da Col kısaysa `.extended ` kullanabilirsin. daire sekli yerine stadium sekli olur.
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

- Style classi kullanmanı gerektirmeyen bir diğer özellikse default temalardır. Belirli özelliklerini `copyWith` ile değiştirebilirsin.

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

- Material app içindeki `title` uygulamayı diğer uygulamalarla goruntulerken gozuken ismidir.
- Material app projede bir tane olmalıdır. Aksi durumda routing bozulur vs.
- Container içindeki `constraint` kullanımı
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

- `padding` içerden uzaklık `margin` dıştan uzaklık
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

- `FloatingAcionButon` centerde hoş duruyo
- `bottomsheet` asagidan yukarı doğru açılan bir pencere , extendbody
- `bottomnavbarlara` da üstteki classlardaki stylelar aktarılabilir.
- buton türleri bunların onpressini null yaparsan buton aktif olmaz. enable olayı gibi . Text butonda renk degistirme yerine outlineda daha kolay
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
- appbarda `leading` uctaki icon, `actions` sondaki sey ,`centertitle` onemli, bg kaldırma icin transparent yap ve elevation 0 yap,`systemoverlaystyle` ile statusbar rengini değiştir(statusbar appbarın da üstü olan kısım appbar ile status renkleri aynı olmalı)) ,
- `automaticallyImplyLeading`: false yaparsan appbardaki geri butonu kaldırılır.
- projedeki her appbar için aynı olan özellikleri mainde `themedataya` `copywith` ile ekleyebilirsin.Copywith parenttan alır eğer iletirse kendi özelliklerini ekler childa salar.
- parametreler arasından {} içindekiler harici rqeuired olanlar. -`outlinebuttnları` kullanmayı unutma diğer hallerine kıyasla daha iyi
- renkleri isimlendirmek için https://chir.ag/projects/name-that-color/ kullanabilirsin.
- static yaparken dikkatli ol dedi,
- eğer renk verirken temadan alırsan tema değişiminde ona uygun bir renk değişimi olur yorulmazsın.
- hani color: Colors.red yaparken `enumaration` kullanılıyo kendi renklerini de oluşturabilirsin.
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

-eger sadece o file üzerinden erişilecekse file private yap \_ ile başlat

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

- Ayrıca yine mainde `cardTheme` ile cardlar için genel bir tema oluşturabiliriz.
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
- Image eklerken `Image.network` olanında `errorBuilder` kullanıp placeholder ekleyebiliriz.
  ornek:

```dart
errorBuilder: (context, error, stackTrace) => const Icon(Icons.abc_outlined),
```

- Text() içindeki metne sağ tıklayıp `extract local variable` yapıp ayırabiliriz.Onu da yukarı at. karmaşık gözükmesin.

- `with` ile utility ekleme yontemi ve `styleFrom` `primary` ve `shape` özellikleri
  - birden fazla kez kullanılabilecek bir buton benzer özelliklerdeyse aynı ozellikleri belirlenir. Değişken özellikleri de kendimiz ekleriz. -` final void Function() onPressed;` ile butonun basılması durumunda ne olacağını belirleriz. void callbakc function.

```dart
// ornek Utility ekleme yöntemi
class CustomFootButton extends StatelessWidget with _ColorsUtility, _PaddingUtility //<<< with _ColorsUtility, _PaddingUtility
{
  CustomFootButton({Key? key, required this.title, required this.onPressed}) : super(key: key);//<<< required this.onPressed
  final String title;
  final void Function() onPressed;
  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
        style: ElevatedButton.styleFrom(primary: redColor, shape: const StadiumBorder()),//<<<
        onPressed: onPressed,
        child: Padding(
          padding: normal2xPadding,
          child: Text(
            title,
            style: Theme.of(context).textTheme.subtitle2?.copyWith(color: white, fontWeight: FontWeight.bold),//<<< white
          ),
        ));
  }
}
class _ColorsUtility {
  final Color redColor = Colors.red;
  final Color white = Colors.white;
}
class _PaddingUtility {
  final EdgeInsets normalPadding = const EdgeInsets.all(8.0);
  final EdgeInsets normal2xPadding = const EdgeInsets.all(16.0);
}
```

- indikator eklemek için `CircularProgressindicator` kullanabilirsin , yine `themeData` üzerinden `progressindicatortheme` ile kişiselleştirebilirsin.
- `listtile` da twitterda postlar altalta ya onun gibi. özellikleri , title subtitle leading trailing bir de buradaki özelliklere istediğin widgeti ekleebilirsin yani title a image vs. `listTileTheme` ile de tema oluşturabilirsin.
- heryerde kullabileceğin componentleri `core` klasöründe , projeye özel olanları da `product` klasöründe tut.
- required kısmında eğer veri gelmezse varsayılan değer atamak için{ ... ,`this.degisken= deger`} sekline yapabilirsin.
- girilen height bilgisi de aynı sekilde classlarda tutulabilir.
- stack te positioned kullanarak childlerin yerini ayarlayabilirsin. positioned.fill ile de childin tamamını kaplayabilirsin. altına bir positioned daha atarsan alttaki üstte gözükür.
- statelessswidget a sağ tıklayıp statefulwidget yapabalirsin.
- widgeta sağ tıklayıp `extract widget` yaparsan ayrı bir widget oluşturur. \_ koy basa
- benzer kodları olabildiğince birleştirmeyi dene
- setstatei kullandığın widgetin güncellemesi kendisiyle sınırlı olsun ekranı yenilemesin.Bunun için `product ` a orn counterbutton eklersin orda widgeti yazarsn
- HER PROJEDE STRINGLERI KULLANIRSIN GENELDE BU YUZDEN PRODUCT KLASÖRÜNE `language` klasörü EKLE içine de language_items.dart oluştur. orda tüm stringleri tut.
  ornek:

```dart
class LanguageItems {
  static const welcomeTitle = "Merhaba";
  static const mailTitle = "Mail";
}
```

-PageView ile sayfalar arası geçiş sağa sola kaydırarak (default sağ sol)yukarı aşağı kaydırarak yapabilirsin. PageView.builder ile de sayfa sayısını belirleyebilirsin.

- ornek ozellikler controller : PageController (viewPortFraction: 0.8, initialPage: 1, keepPage: true, pageSnapping: true, reverse: false,)
- baska widget ile pageview controllerine etkimek için `final PageController _pageController = PageController();  _pageController.jumpToPage(1); ` gibi kullanabilirsin.

ornek

```dart
PageView(
        children: [
          //burada direct yaptığın scaffoldlu sayfaları da koyarsın widgetleri de
          Container(
            color: Colors.red,
            child: Center(child: Text("1")),
          ),
          Container(
            color: Colors.blue,
            child: Center(child: Text("2")),
          ),
        ],
)
PageView.builder(
        itemCount: 3,
        itemBuilder: (context, index) {
          return Container(
            color: Colors.red,
            child: Center(child: Text(index.toString())),
          );
        },
      ),
```

- widget keylerin orda` {.., required this.metin}` yaparsan altında da `final String message` koyarsa stateful widget kısmında metine erşimek için `widget.metin` şeklinde kullanabilirsin.
- initState widgetin constructorudur .Widget daha cizilmeden önce çalışır.
  -final değeri atayamazsan late eklemen lazım initstate gibi constructorda atancaksa
- `didChanhgeDependencies` initstateden sonra , widgetin build metodu çalışmadan önce çalışır.
  ornek

```dart
 @override
  void didChangeDependencies() {
    super.didChangeDependencies();
    print('c');
  }
```

- `dispose()` widgetin ömrü bittiğinde çalışır. kullanılan controllerlar burada dispose edilir.
  ornek

```dart
 @override
  void dispose() {
    super.dispose();
    print('d');
  }
```

-textfield a decoration eklemek için ornek `decoration: InputDecoration(hintText: "hint", labelText: "label", border: OutlineInputBorder(),)` şeklinde ya da yapabilirsin.
-Metin uzunluğuna göre rengi değişen kutu BuildCounter ile yapılabilir.

```dart
buildCounter: (BuildContext context, {int? currentLength, bool? isFocused, int? maxLength}) {
                return _animatedContainer(currentLength);
              },
              ///...
_animatedContainer(
  //..
     color: Colors.green[100*(currentlength??0)],
  //..
    ),
```

-AnimatedContainer ile animasyonlu container oluşturabilirsin. geçiş hoş olur vs
-keyboard type mail num vs ayarla işe yarar. MİMMAX LİNE VS DE EKLEYEBİLİN
ornek

```dart
//... BU STYLERI DA THEME DAN VS YAPABILIN
 FocusNode focusNodeTextFieldOne = FocusNode();
 //...

//...
              keyboardType: TextInputType.emailAddress,
              autofocus: true,
              autofillHints: const [AutofillHints.email],
              focusNode: focusNodeTextFieldOne,
              inputFormatters: [TextProjectInputFormmater()._formmatter],
              textInputAction: TextInputAction.next,//BU ENTERA TIKLANINCA   ALTTAKİ TEXTFIELD A GEÇİŞİ SAĞLAR
              decoration: _InputDecarotor().emailInput,
//...

class _InputDecarotor {
  final emailInput = const InputDecoration(
    prefixIcon: Icon(Icons.mail),
    border: OutlineInputBorder(),
    labelText: LanguageItems.mailTitle,
  );
}
```

- sorunu ya da widgeti ya da ozelligi anlamazsan kod icine bak belki anlarsın:D

- codingde index şartları hazırlarken` ==0` gibi durumlar yerine enum `_pageColors{red,yellow,blue }` gibi bişi yapıp` == _pageColors.red.index` yapman okuyuculuğu vs daha iyi etkiler.

- ui yani build içinde kod olmamalı dikkat et , `extract method ` kullan
- nullableda diğer senaryoları alt widget yapmalı böylece daha kullanıalabilir olr
- üstten assa veri gidio da alltan üste gitmezse `didUpdateWidget` soyle seler var
  orneka

```dart
@override
  void didUpdateWidget(covariant ColorDemos oldWidget) {
    super.didUpdateWidget(oldWidget);
    if (widget.initialColor != _backgroundColor && widget.initialColor != null) {
      changeBackgroundColor(widget.initialColor!);
    }
  }
    void changeBackgroundColor(Color color) {
    setState(() {
      _backgroundColor = color;
    });
  }

```

- widget sığmazsa die `fittedBox` kulanabilin
- divider ve spacer
- `listliew` scroll yapmana yarar özellik olarak üstten `paddingi` var `zero` ile sıfırlaryabilirsin

  - `listview` içindeki daha ekranda olmayan widgetler çalışmaz ekrana geldiği an `init` gittiği an `dispose` çalışır.
  - `shrinkwrap` sizei belli olmayan widgetin sizeini bi şekilde ayarlio
  - `builder` ekranda olanları initliyo `separotrbuilder` ayraç da eklio aralarına
  - `itemCount` sayısını vermek istersen
  - itemCount ekrandaki widget sayısından fazlaysa item count kadar init olur ancak Column'u Sizedbox ile sınırlandırırsan ekrandaki widget sayısı kadar init olur. 15 ten 4 e gibi
    ornek

  ````dart
  ListView.separated(
        separatorBuilder: (context, index) {
          return const Divider(color: Colors.white);
        },
        itemBuilder: (context, index) {
          return SizedBox(
            height: 200,
            child: Column(
              children: [Expanded(child: Image.network('https://picsum.photos/200')), Text('$index')],
            ),
          );
        },
        itemCount: 15,
      ),
      ```

  ````

- Image sığmadığında expanded ile sarmalayanzi
- https://github.com/VB10/Flutter-Full-Learn/blob/main/lib/demos/my_collections_demos.dart güzel ornek

```dart

class MyCollectionsDemos extends StatefulWidget {
  const MyCollectionsDemos({Key? key}) : super(key: key);
  @override
  State<MyCollectionsDemos> createState() => _MyCollectionsDemosState();
}

class _MyCollectionsDemosState extends State<MyCollectionsDemos> {
  //buradan almak üzere olacağımız itemleri initle CollectionItems() ile alıyoruz.
  late final List<CollectionModel> _items;
  @override
  void initState() {
    super.initState();
    _items = CollectionItems().items;
  }
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: ListView.builder(
        itemCount: _items.length,
        padding: PaddindUtility().paddingHorizontal,
        itemBuilder: (context, index) {
          return _CategoryCard(model: _items[index]);
          //burada karta indexinci item veriliyor kartta model- (indexinci item) - denmiş buna
        },
      ),
    );
  }
}
//burada modelimiz yani CollectionModel tipindeki modelimiz geliyor.
class _CategoryCard extends StatelessWidget {
  const _CategoryCard({
    Key? key,
    required CollectionModel model,
  })  : _model = model,
        super(key: key);

  final CollectionModel _model;
  @override
  Widget build(BuildContext context) {
    return Card(
      margin: PaddindUtility().paddinBottom,
      child: Padding(
        padding: PaddindUtility().paddingGeneral,
        child: Column(
          children: [
            Image.asset(_model.imagePath, fit: BoxFit.fill),
            Padding(
              padding: PaddindUtility().paddingTop,
              child: Row(
                mainAxisAlignment: MainAxisAlignment.spaceBetween,
                children: [Text(_model.title), Text('${_model.price} eth')],
              ),
            )
          ],
        ),
      ),
    );
  }
}

class CollectionModel {
  final String imagePath;
  final String title;
  final double price;
  CollectionModel({required this.imagePath, required this.title, required this.price});
}

class CollectionItems {
  late final List<CollectionModel> items;
  CollectionItems() {
    items = [
      CollectionModel(imagePath: ProjectImages.imageCollection, title: 'Abstract Art', price: 3.4),
      CollectionModel(imagePath: ProjectImages.imageCollection, title: 'Abstract Art2', price: 3.4),
    ];
  }
}

```

- `navigate` kodunu direkt eklemek yerine `mixin`(constructorsuz class) olusturabliriz onu da widgeta `with` ile ekleyebiliriz

```dart
mixin NavigatorManager {
  void navigateToWidget(BuildContext context, Widget widget) {
    Navigator.of(context).push(
      MaterialPageRoute(
          builder: (context) {
            return widget;
          },
          fullscreenDialog: true,
          settings: const RouteSettings()),
    );
  }

  class _NavigationLearnState extends State<NavigationLearn> with NavigatorManager {//with NavigatorManager

    ...
    onpressed:{
      navigateToWidget(context,nextPageWidget());// navigateToWidget(context,nextPageWidget())
    }
  }
```

- navigate `push ` Type: Future<dynamic> Function(Route<dynamic>)
  - Future oldğu için await var
  - birinden `props` olarak diğerinden ise `pushtan` alarak iletim sağlananzi

```dart
Future<T?> push<T extends Object?>(Route<T> route)
//Future Generic pushtan geri dönen değer var. Bunu tutabiliriz.
```

```dart
Future<T?> navigateToWidgetNormal<T>(BuildContext context, Widget widget) {
  return Navigator.of(context).push<T>(
    MaterialPageRoute(
        builder: (context) {
          return widget;
        },
        settings: const RouteSettings()),
  );
}
```

```dart
//T yerine burada kendi tipimizi giriyoruz.
 onPressed: () async {
            final response = await navigateToWidgetNormal<bool>(
                context, NavigateDetailLearnDart(isOkey: selectedItems.contains(index)));
```

- integer list dizisi `List<int> selectedItems = [];` ile yapılr
  - `.add()` `.remove` `.contains()` gibi methodları da vardır

## Modellerle ilgili güzel notlar ve örnekler.
``` dart
/bu init edilmediğinden null olabileceğinden ağlıyor.
/*
class PostModel {
  int userId;
  int id;
  String title;
  String body;
}
*/
//bu da ağlamıyo çünkü null gelebilir diyoruz. Bundan gelen verileri ??"" ile kullan ! kullanma.
class PostModel1 {
  int? userId;
  int? id;
  String? title;
  String? body;
}

//Bunda ise nullable yok ağlar ancak constructor ile yaparsın. Bu variablelar uygulama contruct edildiğinde gelecek. ve gider
class PostModel2 {
  int userId;
  int id;
  String title;
  String body;
  PostModel2(this.userId, this.id, this.title, this.body);
}

// Bunu final yapıyorsun . YİNE AĞLIYOR. Çünkü hala init değil. Final olmasından dolayı sadece Contruct zamanında atanacak bir model yapmış oluyurz. ve gider.
class PostModel3 {
  final int userId;
  final int id;
  final String title;
  final String body;

  PostModel3(this.userId, this.id, this.title, this.body);
}

// burada ağlıyor, final yapan yine ağlıyor.  Named girsin istiyorsan yani model(a:"assd", b:"asdasd",c:31 ) vs. Contructora alıp değişkenleri { } içine alıyorsun. BAŞLARINA REQUIRED KOYUYORSUN.ve gitti.
class PostModel4 {
  final int userId;
  final int id;
  final String title;
  final String body;

  PostModel4({
    required this.userId,
    required this.id,
    required this.title,
    required this.body,
  });
}

//ÜSTTEKI GİBİ NAMED GİRİYORuz ama fark constructorda this yerine type giriyoruz. yine ağlıyor. constructor sonuna ): _degisken=degisken; şeklinde yazıyoruz. ve gitti.
class PostModel5 {
  final int _userId;
  final int _id;
  final String _title;
  final String _body;

  PostModel5({
    required int userId,
    required int id,
    required String title,
    required String body,
  })  : _userId = userId,
        _id = id,
        _title = title,
        _body = body;
}

//5teki  ustteki gibi named alıyor. farkı sonda : _degisken=degisken; yerine classta late kullanıyoruz. ve gitti.
class PostModel6 {
  late final int _userId;
  late final int _id;
  late final String _title;
  late final String _body;

  PostModel6({
    required int userId,
    required int id,
    required String title,
    required String body,
  }) {
    _userId = userId;
    _id = id;
    _title = title;
    _body = body;
  }
}

//6dan farkı required yok. ağlıyor initial value ekliyoruz constructorda = 31; gibi
class PostModel7 {
  late final int _userId;
  late final int _id;
  late final String _title;
  late final String _body;

  PostModel7({
    int userId = 31,
    int id = 21,
    String title = "Ferit",
    String body = "adad",
  }) {
    _userId = userId;
    _id = id;
    _title = title;
    _body = body;
  }
}

//eğer bu postmodeliniz içinni doldurmadoğonız textfieldlarnız servisten bekleyenlerini.BUNLAR HEP NULL GELEBİLİR.  cONSTRUCTURDA OPTIONAL ANLAMINDA { } sarmalarsın . VE GİTTİ.
class PostModel8 {
  final int? userId;
  final int? id;
  final String? title;
  final String? body;

  PostModel8({this.userId, this.body, this.id, this.title});
}


// Generate Copywith kodu ampule tıklion genreate copywith ile sadece istediğin özelliği ekliyon ya da değiştiriyon.
class PostModel9 {
  final int? userId;
  final int? id;
  final String? title;
   String? body;

  PostModel9({this.userId, this.body, this.id, this.title});
  void updateBody(String? data) {//normalde direkt baska sayfda postmode.copywith(body: "asdasd") yaparsın.  
    //data.length hata verir
    if (data != null&& data.isNotEmpty) {//
      //data.length hata vermez burada body null değil
      body = data;

    }
    //burada null olabliir.
  }

  PostModel9 copyWith({
    int? userId,
    int? id,
    String? title,
    String? body,
  }) {
    return PostModel9(
      userId: userId ?? this.userId,
      id: id ?? this.id,
      title: title ?? this.title,
      body: body ?? this.body,
    );
  }
}

```
``` dart 
class ModelLearnView extends StatefulWidget {
  const ModelLearnView({Key? key}) : super(key: key);

  @override
  State<ModelLearnView> createState() => _ModelLearnViewState();
}

class _ModelLearnViewState extends State<ModelLearnView> {
  var user9 = PostModel9(
      body:
          "aaaaa"); //fianl olmaz değişebilir veri olmalı var ya da PostModel gibi type
  @override
  void initState() {
    // TODO: implement initState

    final user1 =
        PostModel1() // model sonuna .. ile direkt degistkenlere erisilebiliyor. fnial da değil tekrar atama yapılabiliriyo
          ..userId = 31
          ..title = "aaa"; //nullable olduğundan bişi istemedi
    user1.body = "body";

    final user2 = PostModel2(31, 15, "aaa",
        "body"); //nullable değil ama constructor var fnial da değil tekrar atama yapılabiliriyor
    user2.userId = 21;

    final user3 = PostModel3(31, 15, "aaa",
        "body"); ////nullable değil ama constructor var final olduğundan tekrar atama yapamıyoruz.
    //user3.userId = 21; olmaz X
    final user4 = PostModel4(
        userId: 31,
        id: 15,
        title: "aaa",
        body:
            "body"); //named giriyoruz. final olduğundan tekrar atama yapamıyoruz.
    //user4.body="body"; //olmaz X

    final user5 = PostModel5(
        userId: 31,
        id: 15,
        title: "aaa",
        body:
            "body"); //named giriyoruz. final olduğundan tekrar atama yapamıyoruz.
    //user5. yapınca degiskenler gözükmüyor çünkü _ private

    final user6 = PostModel6(
        userId: 31,
        id: 15,
        title: "aaa",
        body:
            "body"); //named giriyoruz. final olduğundan tekrar atama yapamıyoruz.
    //user6. yapınca degiskenler gözükmüyor çünkü _ private
    final user7 = PostModel7();
    //user7.userId = 31;   yapınca degiskenler gözükmüyor çünkü _ private

    final user8 = PostModel8(body: "aaaaa");
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          setState(() {
            user9 = user9.copyWith(title: "titleyeni");
            user9.updateBody(null);//mukemmel bisi eğer veri gelirse veri değişir null gelirse değişmez
          });
        },
      ),
      appBar: AppBar(
        title: Text(user9.title ??
            "NULL GELENZİ"), //null gelirse null gelmezse title yazdır
      ),
      body: Container(),
    );
  }
}

```