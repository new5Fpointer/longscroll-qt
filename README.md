# longscroll-qt

![icon](doxygen/img/longscroll-qt-icon-128.png)

> **Note:** This is a Qt 6 / CMake port of the original [longscroll-qt](https://github.com/TripleWhy/longscroll-qt) by Yannick Mueller.
> The original library uses Qt 5 and qmake; this fork migrates to **Qt 6** with a **CMake** build system while keeping the API compatible.

longscroll-qt is a C++ library to create very long, fast and responsive scrollable widgets in Qt.

The longscroll widget can visualize a large list of items, similar to a QAbstractItemView.
The main differences are that longscroll-qt is responsive, has much more flexible layout options and uses real widgets to display items.
This allows easy user interaction and simple customization as you can for example use the Qt designer to create an item widget.
longscroll-qt also offers a fully customizable navigator widget wich is shown between two rows, creating a complete google-images-like view.

The library was tested and works with millions of image items.

## API Docs

Online documentation for the current release can be found at <https://triplewhy.gitlab.io/longscroll-qt/doc/>.

You can also [download](../../releases) a html or qhp version to integrate into Qt Assistant and Qt Creator.

## Examples

The library comes with two [examples](examples). To understand the behavior best, keep resizing the window.

- [examples/simple](examples/simple) sets up a simple program using only a few lines of code to get you up running fast.
- [examples/demo](examples/demo) deomstrates the power of longscroll-qt by providing a gui that lets you dynamically change nearly every setting to see what it does.

The documentation of [longscroll::ContentWidget](https://triplewhy.gitlab.io/longscroll-qt/doc/classlongscroll_1_1_content_widget.html) can give a good overview of what longscroll-qt can do, as most of its functionality is provided by that class.

## Stylesheets

longscroll-qt widgets can be styled like any other widget. Since longscroll-qt uses a namespace, `longscroll` by default, stylesheets have to specify it too. For example:

```css
longscroll--ContentWidget {
	background: blue;
}
longscroll--ImageWidget {
	background: yellow;
}
```

## Requirements

longscroll-qt needs **Qt 6** and a **C++17** compatible compiler. It can run on all systems that have Qt, including Linux, Windows and macOS.
Building the documentation additionally requires doxygen and graphviz.

On Ubuntu all requirements (including docs) can be installed with the following packages:

```
# apt-get install build-essential clang qt6-base-dev qt6-base-dev-tools qt6-tools-dev doxygen graphviz
```

## Compiling

longscroll-qt uses **CMake** (minimum version 3.16). You can either open the project in Qt Creator / Visual Studio with CMake support, or build from the command line.

Compiling from the command line could be for example like this:

```
cd src
cmake -B build -S . -DCMAKE_PREFIX_PATH=<Qt6 path>
cmake --build build

# Build and run examples:

cd ..
cmake -B build -S . -DCMAKE_PREFIX_PATH=<Qt6 path>
cmake --build build

# Run examples:
cd build/examples/simple
./simple <some dir>
# for example:
./simple ~/Pictures/

cd ../demo
./demo [some dir [demo number]]
```

Alternatively you can use CMake presets. Create a `CMakeUserPresets.json` in the project root with your Qt path:

```json
{
  "version": 3,
  "configurePresets": [
    {
      "name": "default",
      "cacheVariables": {
        "CMAKE_PREFIX_PATH": "/path/to/qt/6.x.x/gcc_64"
      }
    }
  ]
}
```

Then build with:

```
cmake --preset default
cmake --build --preset default
```

## Screenshots

This library can best be experienced by running and resizing the demo program.
The following are some layout possibilities from the documentation (they are actual screen shots):

![layout 1](doxygen/img/layout1.png)
![layout 2](doxygen/img/layout2.png)
![layout 3](doxygen/img/layout3.png)
![layout 4](doxygen/img/layout4.png)
![layout 5](doxygen/img/layout5.png)
![layout 6](doxygen/img/layout6.png)

Alright here are some real screenshots anyway:

![screenshot 1](doxygen/img/screen01.jpg)

![screenshot 2](doxygen/img/screen02.jpg)

![screenshot 3](doxygen/img/screen04.jpg)

![screenshot 4](doxygen/img/screen06.jpg)

![screenshot 5](doxygen/img/screen05.jpg)

## License

longscroll-qt is licensed under AGPL v3. (Contact me if you need a commercial license.)
