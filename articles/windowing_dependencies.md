# The long story of ÖbEngine and dependencies : Windowing

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

Of course those are **my** needs and the criteria listed above might not be the definition of perfection for someone else.

## [SFML](https://www.sfml-dev.org) : The current choice

![SFML logo](https://www.sfml-dev.org/images/logo.png)

SFML will appear quite a lot in this blog post series because it is the solution I use for many categories.

I started using SFML at first because the API was easy to understand and the documentation / examples were well made.

### Pros

- I know SFML and already use it in ÖbEngine
- Documentation is top-notch
- Integrates well with other SFML components
- You can easily retrieve a working OpenGL context with the version of your choosing
- Works on Windows, Linux, MacOS, Android, iOS
- Permissive license (zlib/png)

### Cons

- No support for retrieving screen's refresh rate
- Multiple monitors are not supported
- Doesn't support Vulkan nor OpenGL ES
- Android port is extremely painful
- Doesn't support webassembly
- Too big of a dependency to embed in the repository
- Fewer and fewer contributions
- Too big of a dependency to embed in the repository

My biggest concern is that SFML seems to be dying slowly. Even if SFML 2.6 is supposed to be released soon, the repository is getting less and less contributions. The main contributor being gone doesn't help either.

![SFML Git contributions](https://raw.githubusercontent.com/ObEngine/obengine.github.io/main/images/sfml_git_contributions.png)

## [SDL](https://www.libsdl.org/) : The default choice

![SDL logo](https://www.libsdl.org/media/SDL_logo.png)

When is comes to creating a cross-platform window, SDL is often a go-to solution for many developpers.

### Pros

- Support for Windows, Linux, MacOS, Android, iOS, HTML5, PS Vita and many more
- Can create an OpenGL, OpenGL ES, Vulkan, DirectX context
- Multimedia library of choice in the industry, well maintained
- Well documented library
- Support for multiple monitors as well as getting the refresh rate
- Permissive license (zlib)

### Cons

- The interface is C code, you have to manage the lifetime of your objects
- Too big of a dependency to embed in the repository

SDL is still around and kicking, with a health amount of git contributions.

![SDL Git contributions](https://raw.githubusercontent.com/ObEngine/obengine.github.io/main/images/sdl_git_contributions.png)

## [GLFW](https://www.glfw.org/) : The specialized one

![GLFW logo](https://www.saashub.com/images/app/service_logos/38/b48cc85cebb2/large.png?1553244024)

GLFW is a well known library that specialize in window creation and event polling.

### Pros

- Support for multiple monitors as well as getting the refresh rate
- Support for Windows, Linux, MacOS
- Permissive license (zlib/png)

### Cons

- No support for mobile platforms (Android, iOS) nor HTML5
- Not modern C++

![GLFW Git contributions](https://raw.githubusercontent.com/ObEngine/obengine.github.io/main/images/glfw_git_contributions.png)

## [GLFM](https://github.com/brackeen/glfm) : The little brother

#### Pros

- Permissive license (zlib)

## [Freeglut](http://freeglut.sourceforge.net/) : The old fashioned

#### Pros

- Permissive license (MIT)

## [CrossWindow](https://github.com/alaingalvan/CrossWindow) : The youngster

#### Pros

- Permissive license (MIT)

### [Cinder](https://libcinder.org/) : More than you asked for

#### Pros

- Permissive license (BSD)

## [Magnum Graphics](https://magnum.graphics/) : On the shoulder of giants

Magnum Graphics is not a windowing library per se, it wraps other windowing applications such as SDL2, GLFW or GLX in a user-friendly interface. It provides glue-code for some platforms like Android so you don't have to deal with that yourself.

There would be a lot of advantages in using Magnum graphics for other components as well so it's a serious option to consider.

#### Pros

- Permissive license (MIT)
- Support for Windows, Linux, MacOS, Android, iOS, HTML5
- Can create an OpenGL, OpenGL ES or Vulkan context
- Well documented library

#### Cons

- No support for multiple monitors as well as getting the refresh rate

## [Qt](https://www.qt.io/) : The mastodont

#### Cons

- Huge dependency
- Non-permissive license (LGPL)

## [Gamedev Framework](https://gamedevframework.github.io/) : Best of both worlds ?

Gamedev framework is still a relatively young project (2016) it has the same scope as the SFML.

#### Pros

- The API looks like a lot the SFML one, meaning easier migration
- Cool additional features missing from SFML (Better gamepad support being an example)
- Supports Windows, MacOS, Linux, Android, iOS
- Support for multiple monitors as well as getting the refresh rate
- Permissive license (zlib/png)

#### Cons

- The library relies on a single main contributor, bus factor is pretty low
- Doesn't support HTML5
- Library is not well known, not a lot of documentation / examples except the provided ones
- Limited to usage of OpenGL 3.3 or OpenGL ES 2.0

## [StormKit](https://gitlab.com/Arthapz/stormkit) : The friendly one

#### Pros

- Permissive license (MIT)

## [FLTK](https://www.fltk.org) : The dusty one

## [WxWidgets](http://www.wxwidgets.org/) : Not the right tool for the job



## All the other ones

While searching for all these libraries, I stumbled upon a few interesting ones but I judged them not mature enough to have a section of their own.

- [Ecere SDK](http://ecere.org/) : Seems to be a complex environment with its own language, not what I need
- [Aglet](https://github.com/elucideye/aglet) : Abandonned
- [kelgin-window](https://github.com/keldu/kelgin-window) : Not mature enough
- [XGTL](https://github.com/benswift/XTGL) : Abandoned
- [AWML](https://github.com/8infy/AWML) : Abandoned

