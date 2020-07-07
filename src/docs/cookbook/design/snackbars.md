---
title: Display a snackbar
description: How to implement a snackbar to display messages.
prev:
  title: Add a drawer to a screen
  path: /docs/cookbook/design/drawer
next:
  title: Export fonts from a package
  path: /docs/cookbook/design/package-fonts
js:
  - defer: true
    url: https://dartpad.dev/inject_embed.dart.js
---

Khi một số thao tác xảy ra, việc thông báo cho người dùng sẽ khá là có ích.
Ví dụ, khi người dùng xoá một tin nhắn trong danh sách, bạn sẽ muốn thông báo với họ rằng tin nhắn đó đã được xoá. Hơn nữa, bạn còn có thể cho họ lựa chọn để hoàn tác việc xoá tin nhắn đấy.

Trong Material Design, đây là công việc của [`SnackBar`][].
Phương thức này áp dụng snackbar qua những bước sau:

  1. Tạo `Scaffold`.
  2. Hiển thị `SnackBar`.
  3. Cung cấp một thao tác tuỳ chọn.

## 1. Tạo `Scaffold`

Khi tạo các ứng dụng tuân theo các quy tắc Material Design, hãy thiết kế cho 
ứng dụng của bạn một giao diện phù hợp.
Ví dụ này hiển thị `Snackbar` ở phía dưới cùng của màn hình, 
mà không chồng lên các widgets quan trọng khác, như `FloatingActionButton`.

 [`Scaffold`][], từ [material library][],
 tạo giao diện này và đảm bảo rằng các widgets quan trọng
 không chồng lên nhau.

<!-- skip -->
```dart
Scaffold(
  appBar: AppBar(
    title: Text('SnackBar Demo'),
  ),
  body: SnackBarPage(), // Complete this code in the next step.
);
```

## 2. Hiển thị `SnackBar`

Sau khi tạo xong `Scaffold`, ta sẽ hiển thị `SnackBar`.
Đầu tiên, tạo `SnackBar`, rồi hiển thị nó thông qua `Scaffold`.

<!-- skip -->
```dart
final snackBar = SnackBar(content: Text('Yay! A SnackBar!'));

// Find the Scaffold in the widget tree and use it to show a SnackBar.
Scaffold.of(context).showSnackBar(snackBar);
```

## 3. Cung cấp một thao tác tuỳ chọn

Bạn có thể muốn cung cấp cho người dùng một thao tác khi
SnackBar được hiển thị.
Ví dụ, nếu người dùng vô tình xoá một tin nhắn,
họ có thể dùng thao tác tuỳ chọn trong SnackBar để hồi phục
tin nhắn đó.

Đây là ví dụ của việc cung cấp
thêm một `thao tác` cho `SnackBar`:

<!-- skip -->
```dart
final snackBar = SnackBar(
  content: Text('Yay! A SnackBar!'),
  action: SnackBarAction(
    label: 'Undo',
    onPressed: () {
      // Some code to undo the change.
    },
  ),
);
```

## Ví dụ

{{site.alert.note}}
  Trong ví dụ này, SnackBar sẽ được hiển thị khi người dùng ấn một nút.
  Để tìm hiểu thêm về thao tác của người dùng,
  xem phần [Gestures][] của cẩm nang.
{{site.alert.end}}

```run-dartpad:theme-light:mode-flutter:run-true:width-100%:height-600px:split-60:ga_id-interactive_example
import 'package:flutter/material.dart';

void main() => runApp(SnackBarDemo());

class SnackBarDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'SnackBar Demo',
      home: Scaffold(
        appBar: AppBar(
          title: Text('SnackBar Demo'),
        ),
        body: SnackBarPage(),
      ),
    );
  }
}

class SnackBarPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Center(
      child: RaisedButton(
        onPressed: () {
          final snackBar = SnackBar(
            content: Text('Yay! A SnackBar!'),
            action: SnackBarAction(
              label: 'Undo',
              onPressed: () {
                // Some code to undo the change.
              },
            ),
          );

          // Find the Scaffold in the widget tree and use
          // it to show a SnackBar.
          Scaffold.of(context).showSnackBar(snackBar);
        },
        child: Text('Show SnackBar'),
      ),
    );
  }
}
```

<noscript>
  <img src="/images/cookbook/snackbar.gif" alt="SnackBar Demo" class="site-mobile-screenshot" />
</noscript>


[Gestures]: /docs/cookbook#gestures
[`Scaffold`]: {{site.api}}/flutter/material/Scaffold-class.html
[`SnackBar`]: {{site.api}}/flutter/material/SnackBar-class.html
[material library]: {{site.api}}/flutter/material/material-library.html
