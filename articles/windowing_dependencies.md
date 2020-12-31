# The long story of ÖbEngine and dependencies : Windowing and Input

A Windowing library is one of the most critical dependency of an engine. It is strongly tied with the input dependency and restricts on which platform your engine might be able to run.

As such, making a bad choice in the choosing of your windowing library could make you lose some time or worse, kill the project.

The definition of a perfect windowing library in my opinion is :

- Cross-platform : Supports Windows, MacOS, Linux (X and Wayland), Android, iOS, HTML5
- Well documented
- Well maintained by multiple contributors
- Supports at least OpenGL / OpenGL ES, ideally DirectX and Vulkan as well
- Made with modern C++
- Supports multiple monitors and can retrieve information from them (resolution, refresh rate)
- Has a permissive license
- Not too heavyweight, possibly embeddable in the repository
- Supports static and dynamic linking
- Good support for keyboard, mouse, joysticks, gamepads, tactile screens

Of course those are **my** needs and the criteria listed above might not be the definition of perfection for someone else.

## One or two libraries ?

A game engine is quite a special software, it needs a lot of dependencies of all kinds. A windowing library is one of those components.

The way I made ÖbEngine would allow multiple windowing libraries to co-exist :

- One (or more) for the Game Engine "Player"
- One (or more) for the Game Engine "Editor"

The game engine editor does not have to be available on all platforms, Windows, Linux and MacOS should be enough. If the editor can run on Android, iOS or HTML5, I would consider that a bonus rather than a priority.

Although, having **one** windowing library for both the player and the editor could make things simpler and there is no real reasons to get two of them.

Ideally, the editor would be "a game" running inside the player, allowing maximum compatibility and flexibility. Godot works that way for example.

## The multimedia libraries

This category regroups all libraries that do more than just managing windows and input. The pros and cons of each library will only discuss about windowing and input though.

### [SFML](https://www.sfml-dev.org) : The current choice

![SFML logo](https://www.sfml-dev.org/images/logo.png)

SFML will appear quite a lot in this blog post series because it is the solution I use for many categories.

I started using SFML at first because the API was easy to understand and the documentation / examples were well made.

My biggest concern is that SFML seems to be dying slowly. Even if SFML 2.6 is supposed to be released soon, the repository is getting less and less contributions. The main contributor being gone doesn't help either.

#### Pros

- I know SFML and already use it in ÖbEngine
- Documentation is top-notch
- Integrates well with other SFML components already in use
- You can easily retrieve a working OpenGL context with the version of your choosing
- Works on Windows, Linux, MacOS, Android, iOS
- Permissive license (zlib/png)
- Supports keyboard, mouse, joystick and gamepad input
- Clipboard support

#### Cons

- No support for retrieving monitor refresh rate
- Multiple monitors are not supported
- Doesn't support Vulkan nor OpenGL ES
- Android port is extremely painful
- Doesn't support webassembly
- Too big of a dependency to embed in the repository
- Fewer and fewer contributions
- Too big of a dependency to embed in the repository
- Does not have gamecontrollerdb like SDL does

#### Stats

SFML contributions are declining in 2020, hopefully it will become more active after 2.6 release.

![SFML Git contributions](https://raw.githubusercontent.com/ObEngine/obengine.github.io/main/images/sfml_git_contributions.png)

### [SDL](https://www.libsdl.org/) : The default choice

![SDL logo](https://www.libsdl.org/media/SDL_logo.png)

When is comes to creating a cross-platform window, SDL is often a go-to solution for many developpers.

#### Pros

- Support for Windows, Linux, MacOS, Android, iOS, HTML5, PS Vita and many more
- Can create an OpenGL, OpenGL ES, Vulkan, DirectX context
- Multimedia library of choice in the industry, well maintained
- Well documented library
- Support for multiple monitors as well as getting the refresh rate
- Permissive license (zlib)
- Excellent input support with a database to handle a great variety of gamepads
- Clipboard support

#### Cons

- The interface is C code
- Too big of a dependency to embed in the repository

#### Stats

SDL is still around and kicking, with a healthy amount of git contributions.

![SDL Git contributions](https://raw.githubusercontent.com/ObEngine/obengine.github.io/main/images/sdl_git_contributions.png)

### [Allegro](https://liballeg.org/) : Yet another fully fledged multimedia library

When I first started C++ gamedev, three multimedia libraries standed out : SDL, SFML and Allegro. Allegro seemed to be less maintained that the other two. Turns out Allegro had a stable release at the beginning of 2020.

#### Pros

- Support for Windows, Linux, MacOS, Android, iOS
- Support HTML5 through SDL backend
- Supports both OpenGL and Direct3D (only up to version 9 though)
- Supports keyboard, mouse, joystick and gamepad input
- Supports touch input
- Support for multiple monitors
- Clipboard support
- The library is still getting attention from multiple contributors (not at the same scale as SDL of course)

#### Cons

- No OpenGL ES, Direct3D > 10 nor Vulkan
- No support for retrieving monitor refresh rate
- The interface is C code
- Too big of a dependency to embed in the repository
- Does not have gamecontrollerdb like SDL does

### [Gamedev Framework](https://gamedevframework.github.io/) : Best of both worlds ?

![gf logo](https://raw.githubusercontent.com/GamedevFramework/gf/master/gf_logo.png)

Gamedev framework is still a relatively young project (2016), its API ressembles the SFML one while extending the feature set.

The Windowing / Input system is directly based on the SDL one, Gamedev Framework acts here as a thin object-oriented layer.

#### Pros

- The API looks like a lot the SFML one, meaning easier migration
- Cool additional features missing from SFML (Better gamepad support being an example)
- Supports Windows, MacOS, Linux, Android, iOS
- Support for multiple monitors as well as getting the refresh rate
- Permissive license (zlib/png)
- Development is quite active

#### Cons

- The library relies on a single main contributor, bus factor is pretty low
- Doesn't support HTML5 explicitly
- Library is not well known, not a lot of documentation / examples except the provided ones
- Limited to usage of OpenGL 3.3 or OpenGL ES 2.0

### [StormKit](https://gitlab.com/Arthapz/stormkit) : The friendly one

![StormKit logo](https://raw.githubusercontent.com/Arthapz/StormKit/master/icons/iOS/AppIcon.xcassets/AppIcon.appiconset/Icon-83.5%402x.png)

#### Pros

- Permissive license (MIT)

### [Magnum Graphics](https://magnum.graphics/) : On the shoulder of giants

Magnum Graphics is not a windowing library per se, it wraps other windowing applications such as SDL2, GLFW or GLX in a user-friendly interface. It provides glue-code for some platforms like Android so you don't have to deal with that yourself.

There would be a lot of advantages in using Magnum graphics for other components as well so it's a serious option to consider.

#### Pros

- Permissive license (MIT)
- Support for Windows, Linux, MacOS, Android, iOS, HTML5
- Can create an OpenGL, OpenGL ES or Vulkan context
- Well documented library

#### Cons

- No support for multiple monitors as well as getting the refresh rate

## The multimedia libraries : Platform support

| Library / Platform | ![SFML Git contributions](https://raw.githubusercontent.com/ObEngine/obengine.github.io/main/images/windows_icon.png) Windows | ![SFML Git contributions](https://raw.githubusercontent.com/ObEngine/obengine.github.io/main/images/macos_icon.png) MacOS | ![SFML Git contributions](https://raw.githubusercontent.com/ObEngine/obengine.github.io/main/images/linux_icon.png) Linux | Android | iOS  |
| ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------- | ---- |
| SFML 2.5           |                                                              |                                                              |                                                              |         |      |
| SDL 2.0.14         |                                                              |                                                              |                                                              |         |      |
| Allegro            |                                                              |                                                              |                                                              |         |      |
| Gamedev Framework  |                                                              |                                                              |                                                              |         |      |
| StormKit           |                                                              |                                                              |                                                              |         |      |
| Magnum Graphics    |                                                              |                                                              |                                                              |         |      |



## GUI libraries

They are not multimedia libraries and the scope is quite different but they might be interesting choice to consider.

### [Qt](https://www.qt.io/) : The mastodont

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/0b/Qt_logo_2016.svg/1200px-Qt_logo_2016.svg.png" alt="Qt logo" style="zoom: 10%;" />

#### Cons

- Huge dependency
- Non-permissive license (LGPL)

### [WxWidgets](http://www.wxwidgets.org/) : Not the right tool for the job

![WxWidgets logo](https://www.wxwidgets.org/assets/img/header-logo.png)

## Dedicated libraries

Those libraries only handle windowing and input, nothing more, nothing less.

### [GLFW](https://www.glfw.org/) : The specialized one

![GLFW logo](https://www.saashub.com/images/app/service_logos/38/b48cc85cebb2/large.png?1553244024)

GLFW is a well known library that specialize in window creation and event polling.

Unlike SFML and SDL, GLFW specializes in window / context creation and input handling which might either be an advantage or a disadvantage. Personally, I don't like to keep all my eggs in one basket.

#### Pros

- Support for multiple monitors as well as getting the refresh rate
- Support for Windows, Linux, MacOS
- Permissive license (zlib/png)
- Lightweight dependency
- Supports keyboard, mouse, joystick and gamepad input
- Clipboard support
- Supports the SDL gamecontrollerdb

#### Cons

- No support for mobile platforms (Android, iOS) nor HTML5
- Not modern C++

#### Stats

![GLFW Git contributions](https://raw.githubusercontent.com/ObEngine/obengine.github.io/main/images/glfw_git_contributions.png)

### [GLFM](https://github.com/brackeen/glfm) : The little brother

#### Pros

- Permissive license (zlib)

### [Freeglut](http://freeglut.sourceforge.net/) : The old fashioned

<img src="http://freeglut.sourceforge.net/images/freeglut_logo.png" alt="FreeGLUT logo" style="zoom:200%;" />

FreeGLUT is an open-source alternative to GLUT, the development started in 1999 making it almost as old as the SDL.

Latest release was made in 2019, the code is very stable but also quite ancient.

#### Pros

- Permissive license (MIT)

#### Cons

- No new features at this point, sticking to GLUT API was one of the project priority
- Mimicks OpenGL state-machine system
- Poor input support

### [CrossWindow](https://github.com/alaingalvan/CrossWindow) : The youngster

<img src="https://raw.githubusercontent.com/alaingalvan/CrossWindow/master/docs/images/cover.png" alt="CrossWindow logo" style="zoom: 67%;" />

#### Pros

- Permissive license (MIT)

### [Cinder](https://libcinder.org/) : More than you asked for

<img src="https://camo.githubusercontent.com/bc307cb2e7d9bd5ae37a1312b0fa3d472ffecec756496acf368a9dad4bd60d4d/68747470733a2f2f6c696263696e6465722e6f72672f646f63732f5f6173736574732f696d616765732f63696e6465725f6c6f676f2e737667" alt="Cinder logo" style="zoom: 25%;" />

#### Pros

- Permissive license (BSD)

### [FLTK](https://www.fltk.org) : The dusty one

![FLTK logo](https://www.fltk.org/images/top-middle.gif)



## All the other ones

While searching for all these libraries, I stumbled upon a few interesting ones but I judged them not mature enough to have a section of their own.

- [Ecere SDK](http://ecere.org/) : Seems to be a complex environment with its own language, not what I need
- [Aglet](https://github.com/elucideye/aglet) : Abandonned
- [kelgin-window](https://github.com/keldu/kelgin-window) : Not mature enough
- [XGTL](https://github.com/benswift/XTGL) : Abandoned
- [AWML](https://github.com/8infy/AWML) : Abandoned

## Conclusion
