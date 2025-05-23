# Widget Control

The widget control provides information about installing and running widget applications.

It also provides functions for the following:

-   Sending update requests to the widget applications
-   Retrieving details of running instances for the same package widget applications

The main features of the `Tizen.Applications.WidgetControl` class includes the following:

-   [Creating a widget control](#create_instance)

    For using the widget control features, you can create a widget control instance with a specific widget ID.

-   [Getting information on widget applications](#getting_information)

    For the widget applications that are installed but not running, you can retrieve widget information.

-   [Listening to widget lifecycle events on widget applications](#listening_events)

    For running widget applications, you can listen to widget application lifecycle events.

-   [Communicating with running widget instances](#communicating_instances)

    For running widget instances, you can trigger an update event, send update data, and retrieve running widget instances detail.

## Prerequisites

To enable your application to use the widget control functionality, follow these steps:

1.  To use the methods and properties of the [Tizen.Applications.WidgetControl](/application/dotnet/api/TizenFX/latest/api/Tizen.Applications.WidgetControl.html) class, include the [Tizen.Applications](/application/dotnet/api/TizenFX/latest/api/Tizen.Applications.html) namespace in your application:

    ```csharp
    using Tizen.Applications;
    ```

2.  To get information on widget application, the application has to request permission by adding the following privilege to the  `tizen-manifest.xml` file:

    ```XML
    <privileges>
       <privilege>http://tizen.org/privilege/widget.viewer</privilege>
    </privileges>
    ```

<a name="create_instance"></a>
## Create a widget control

Create an instance of widget control with an ID of the widget application using the [Tizen.Applications.WidgetControl](/application/dotnet/api/TizenFX/latest/api/Tizen.Applications.WidgetControl.html) class:

```csharp
WidgetControl control = new WidgetControl(Your Widget ID);
```

<a name="getting_information"></a>
## Get information on widget applications

Get the main application ID, package ID, and available scale lists from the control:

```csharp
string mainId = control.MainAppId;
string packageId = control.PackageId;
IEnumerable<WidgetControl.Scale> scales = control.GetScales();
```

<a name="listening_events"></a>
## Listen to widget lifecycle events on widget applications

Add lifecycle listeners on the control to listen to widget lifecycle events:

```csharp
private static void OnCreated(object sender, Tizen.Applications.WidgetLifecycleEventArgs args)
{
    string instanceId = args.InstanceId;
    string widgetId = args.WidgetId;
    /// Widget application is created
}

private static void OnDestroyed(object sender, Tizen.Applications.WidgetLifecycleEventArgs args)
{
    /// Widget application is destroyed
}

private static void OnPaused(object sender, Tizen.Applications.WidgetLifecycleEventArgs args)
{
    /// Widget application is paused
}

private static void OnResumed(object sender, Tizen.Applications.WidgetLifecycleEventArgs args)
{
    /// Widget application is resumed
}

control.Created += OnCreated;
control.Created += OnDestroyed;
control.Created += OnPaused;
control.Created += OnResumed;

string mainId = control.MainAppId;
string packageId = control.PackageId;
IEnumerable<WidgetControl.Scale> scales = control.GetScales();
```

<a name="communicating_instances"></a>
## Communicate with running widget instances

To communicate with the running widget instances, follow these steps:

1.  Operate on the control:
    -   Get running widget instances:

        ```csharp
        IEnumerable<WidgetControl.Instance> instances = control.GetInstances();
        ```

2.  Operate on the instances:
    -   Get details of running widget instances and send an update to the widget application:

        ```csharp
        foreach (WidgetControl.Instance ins in instances) {
            /// Get widget instance content
            var data = ins.GetContent();

            /// Change widget update period
            ins.ChangePeriod(2.0);

            /// Trigger widget update
            ins.ChangeContent(data, true);
        }
        ```

## Related information
  - Dependencies
    -   Tizen 4.0 and Higher
  - API References
    - [Tizen.Applications.WidgetApplication](/application/dotnet/api/TizenFX/latest/api/Tizen.Applications.WidgetApplication) class
    - [Tizen.Applications.WidgetControl](/application/dotnet/api/TizenFX/latest/api/Tizen.Applications.WidgetControl) class
