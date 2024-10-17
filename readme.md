<p align='end'>
  <sub>In Development by <a href="//github.com/bityew">© Bityew</a> (<a href="//github.com/alec1o">© Alecio Furanze</a>)</sub>
  <br>
  <sub>This project serves as the foundation for YewEngine by <a href="//github.com/bityew">© Bityew</a> (<a href="//github.com/alec1o">© Alecio Furanze</a>)</sub>
  <br>
  <sub><a href="//github.com/bityew">© Bityew</a> All Rights Reserved by <a href="//github.com/kezerocom">© Kezero</a> (<a href="//github.com/alec1o">© Alecio Furanze</a>)</sub>
</p>

## BiyML (Biyew Media Library)
BiyML is a C++ library designed to provide a framework for audio manipulation, user input handling (including touch), and window management. This library can be utilized in both C++ and C# applications, making it versatile for game and multimedia development. BiyML offers a simple and efficient interface to facilitate application development.

### Features
- Audio: Loading and playback of audio files.
- Input: Management of keyboard, mouse, and touch inputs.
- Window: Creation and management of application windows.

### Example
- C#
    ```c#
    using BiyML;

    var width = 1280;
    var height = 720;
    var name = "Example Window";
    
    var window = new BitWindow(width, height, name);
    var openGL = new BiyOpenGL(BiyGL.UseLegacy, BiyGL.ES30);
    var inited = window && openGL;
    
    if (inited) window.BindAPI(ref openGL);
    
    while (inited && !window.IsDeadline && BiyTime.WaitFrameRate(60))
    {
        BiyTimer.Refresh();
        BiyInput.Refresh();
        BiyAudio.Refresh();
    
        openGL.ClearColor(BiyColor.Gray);
        openGL.Clear(BiyGL.ColorBufferBit);
    
        if (openGL.Legacy.Begin())
        {
            openGL.Legacy.Color(BiyColor.Red);
            openGL.Legacy.Vertex3(new (0, 0.5, 0));    
            openGL.Legacy.Color(BiyColor.Green);
            openGL.Legacy.Vertex3(new (-0.5F, -0.5F, 0));
            openGL.Legacy.Color(BiyColor.Blue);
            openGL.Legacy.Vertex3(new (0.5F, -0.5F, 0));
    
            openGL.Legacy.End();
        }
    
        window.Refresh();
    }
    ```
- C++
    ```c++
    #include "BiyML.h"
    #include <memory>
    
    int main() {
        auto width = 1280;
        auto height = 720;
        auto name = "Example Window";
    
        auto window = std::make_unique<BiyWindow>(width, height, name);
        auto openGL = std::make_unique<BiyOpenGL>(BiyGL::UseLegacy, BiyGL::ES30);
        
        auto inited = (window != nullptr) && (openGL != nullptr);
    
        if (inited) window->BindAPI(*openGL);
    
        while (inited && !window->IsDeadline() && BiyTime::WaitFrameRate(60)) {
            BiyTimer::Refresh();
            BiyInput::Refresh();
            BiyAudio::Refresh();
    
            openGL->ClearColor(BiyColor::Gray);
            openGL->Clear(BiyGL::ColorBufferBit);
    
            if (openGL->Legacy.Begin()) {
                openGL->Legacy.Color(BitColor::Red);
                openGL->Legacy.Vertex3(BitVector3(0, 0.5f, 0));    
                openGL->Legacy.Color(BitColor::Green);
                openGL->Legacy.Vertex3(BitVector3(-0.5f, -0.5f, 0));
                openGL->Legacy.Color(BitColor::Blue);
                openGL->Legacy.Vertex3(BitVector3(0.5f, -0.5f, 0));
    
                openGL->Legacy.End();
            }
    
            window->Refresh();
        }
    
        return 0;
    }
    ```
