# Hello World Tutorial

This tutorial provides an introduction to NUI and the DALi Animation framework.

The tutorial shows how to create and display "Hello World" using a text label.

A brief description of key NUI concepts is also given.

![The NUI Overview](NUIOverview.md) describes the relationship between NUI and DALi in detail.

## Explanation of tutorial

The following steps are required to display text

+ Initialise the DALi library - TBC with Adeel/Agnelo
+ Create a View - text label showing text
+ Add the text label to the __Window__

## Example code

~~~{.cs}

namespace HelloTest
{
    class Example : NUIApplication
    {
        private TextLabel _text;
        private Window _window;

        public Example():base()
        {
        }

        public Example(string stylesheet):base(stylesheet)
        {
        }

        public Example(string stylesheet, WindowMode windowMode):base(stylesheet, windowMode)
        {
        }

        protected override void OnCreate()
        {
            base.OnCreate();
            Initialize();
        }

        private void Initialize()
        {
            // Connect the signal callback for stage touched signal
            _window = Window.Instance;
            _window.Touch += OnWindowTouched;

            // Add a _text label to the stage
            _text = new TextLabel("Hello World");
            _text.ParentOrigin = ParentOrigin.Center;
            _text.AnchorPoint = AnchorPoint.Center;
            _text.HorizontalAlignment = HorizontalAlignment.Center;
            _text.PointSize = 32.0f;

            _window.GetDefaultLayer().Add(_text);
        }

        // Callback for stage touched signal handling
        private void OnWindowTouched(object sender, WIndow.TouchEventArgs e)
        {
	    _application.Quit();
        }

        static void _Main(string[] args)
        {
            Tizen.Log.Debug("NUI", "Hello world.");
  
            //Example example = new Example("stylesheet", WindowMode.Transparent);
            Example example = new Example();
            example.Run(args);
        }
    }
}

~~~

### Key points

Initialsation ....

To run the application, its main loop should be started. This ensues that images are displayed, events and signals are displatched and captured.

### notes on NUIApplication class

The **NUIApplication** class represents an application that has a UI screen, in addition this class has a default 'stage' - __Window__

The following NUIApplication class member variables are of particular interest:

**_appMode** - application mode (Default, StyleSheetOnly or StyleSheetWithWindowMode

**_stylesheet** - DALi control properties are stylable. The stylesheet contains json markup for the controls.

Style sheets can be written at the device level i.e seperate stylesheets for mobiles and TV's. The stlylesheets
are passed in at the application ctor level (constructors shown here commented out for informational purposes
Alternatively individual stylesheets can be used at the control level.

**_windowMode** - window mode (Opaque or Transparent)


### C# and C++ interaction

In essence the C# API invokes the corresponding C++ API, via the SWIG software tool.

An example:

~~~{.cs}
    public void MainLoop()
        {
            NDalicPINVOKE.Application_MainLoop__SWIG_0(swigCPtr);
            if (NDalicPINVOKE.SWIGPendingException.Pending) throw NDalicPINVOKE.SWIGPendingException.Retrieve();
        }
~~~

