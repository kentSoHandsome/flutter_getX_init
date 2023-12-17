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

# tabbar 某一个item变大
``` dart
bottomNavigationBar: SizedBox(
          height: 76.0, // 设置 BottomNavigationBar 的固定高度
          child: Stack(
            children: [
              Positioned.fill(
                child: Container(
                  color: Colors.transparent, // 设置中间图标的背景色为透明色
                ),
              ),
              Align(
                alignment: Alignment.bottomCenter,
                child: BottomNavigationBar(
                  backgroundColor: Colors.red,
                  items: [
                    BottomNavigationBarItem(
                      icon: Icon(Icons.home),
                      label: 'Home',
                    ),
                    BottomNavigationBarItem(
                      icon: Icon(null),
                      label: '',
                    ),
                    BottomNavigationBarItem(
                      icon: Icon(Icons.person),
                      label: 'Profile',
                    ),
                  ],
                  currentIndex: logic.selectdIndex.value,
                  onTap: (index) {
                    if (index == 1) {
                      return ;
                    }
                    logic.selectdIndex.value = index;
                  },
                ),
              ),
              Align(
                alignment: Alignment.center,
                child: FractionalTranslation(
                  //在 FractionalTranslation 中，
                  // 偏移量的取值范围是从 -1.0 到 1.0。
                  // 当偏移量的 y 值设置为 -0.5 时，
                  // 表示向上偏移了父容器高度的一半。
                  // 这并不等于固定的 30 像素的偏移量，
                  // 因为实际的偏移量取决于父容器的高度。
                  translation: Offset(0.0, -0.3),
                  child: SizedBox(
                    width: 56.0, // 设置中间图标的宽度和高度
                    height: 56.0,
                    child: FloatingActionButton(
                      backgroundColor: Colors.blue, // 设置中间图标的背景色
                      child: Icon(Icons.add, size: 32.0), // 设置中间图标的大小
                      onPressed: () {
                        // 中间图标的点击事件处理
                      },
                    ),
                  ),
                ),
              ),
            ],
          ),
        )
```
