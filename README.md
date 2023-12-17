# flutter_getX_init
flutter的GETX框架的初始化模板库，复制粘贴即可。先引用get插件```get: ^4.6.6```

# main.dart
``` dart
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
import 'package:get/get_navigation/src/root/get_material_app.dart';
import 'package:get/get_navigation/src/routes/transitions_type.dart';
import 'Router/Router.dart';
import 'Router/Pages.dart';
void main() {
  runApp(const MyApp());
}

//移动端(ios & android)需要，web端可以不需要。删掉即可。
var statusBarOverlay = const SystemUiOverlayStyle(
  //设置状态栏的背景颜色
  statusBarColor: Colors.green,
  //状态栏的文字的颜色
  statusBarIconBrightness: Brightness.light,
);

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      debugShowCheckedModeBanner: false,
      initialRoute: Routers.homeTabBar, //初始化的页面。
      title: "任务管理器",
      locale: const Locale("zh", "CN"),//本地化语言
      defaultTransition: Transition.rightToLeftWithFade,
      theme: ThemeData(
          primaryColor: Colors.yellow,
          tabBarTheme: const TabBarTheme(dividerColor: Colors.transparent),
          appBarTheme: AppBarTheme(
              color: Colors.black,
              systemOverlayStyle: statusBarOverlay,
              elevation: 0,
              centerTitle: true,
              // foregroundColor: Colors.black,
              titleTextStyle: const TextStyle(
                  color: Colors.white,
                  fontSize: 18,
                  fontWeight: FontWeight.bold),
              shadowColor: Colors.transparent)),
      getPages: RoutersPages.pages,
      // builder: EasyLoading.init(builder: (context,child) {
      //   return Scaffold(
      //     resizeToAvoidBottomInset: false,
      //     body: GestureDetector(
      //       onTap: () => _hideKeyboard(context),
      //       child: child,
      //     ),
      //   );
      // }),
    );
  }
}

```

# router
``` dart
//Router.dart
class Routers {
  static const homeTabBar = '/tabBar';
}

//Pages.dart
import 'package:get/get_navigation/src/routes/get_route.dart';
import 'package:task_manager/Pages/home_tabbar/home_tabbar_binding.dart';
import 'package:task_manager/Pages/home_tabbar/home_tabbar_view.dart';

import 'Router.dart';

extension RoutersPages on Routers {
  static final pages = [
    GetPage(
      name: Routers.homeTabBar,
      page: () => const HomeTabbarPage(),
      binding: HomeTabbarBinding(),
    ),
  ];
}

```

# other
用GetX插件(Android Studio)创建class，tabbar的build
```dart
@override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.red,
        title: Text('Bottom TabBar Example',style: TextStyle(
          color: Colors.white,
        ),),
      ),
      body: Center(
        child: Text('Page'),
      ),
      bottomNavigationBar: BottomNavigationBar(
        items: [
          BottomNavigationBarItem(
            icon: Icon(Icons.home),
            label: 'Home',
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.search),
            label: 'Search',
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.person),
            label: 'Profile',
          ),
        ],
        // currentIndex: _selectedIndex,
        // onTap: _onItemTapped,
      ),
    );
  }
```
