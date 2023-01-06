# Temelden Zirveye Flutter Derslerinde Aldığım Notlar


- Eğer Row ya da Col kısaysa .extended kullanabilirsin. daire sekli yerine ilac sekli olur.
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

- Style classi kullanmanı gerektirmeyen bir diğer özellikse default temalardır. Belirli özelliklerini copyWith ile değiştirebilirsin.

ornek:

```dart
ThemeData(
   Theme.of(context).textTheme.headline4.copyWith(
     color: Colors.red,
   ),
```
