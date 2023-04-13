<div align="center">
    <img width="100" height="100" src="https://cdn.discordapp.com/attachments/741123537582162020/965619554426437732/wicon.png">
<h1 align="center">DepotDownloaderLib</h1>

Built with:

![Rider](https://img.shields.io/badge/Rider-000000.svg?style=for-the-badge&logo=Rider&logoColor=white&color=black&labelColor=crimson)
![C#](https://img.shields.io/badge/c%23-%23239120.svg?style=for-the-badge&logo=c-sharp&logoColor=white)
![.Net](https://img.shields.io/badge/.NET-5C2D91?style=for-the-badge&logo=.net&logoColor=white)



Uses:
<a href="https://github.com/SteamRE/DepotDownloader">SteamRE/DepotDownloader</a>
<br>
REQUIRES DOTNET 7
</div>

Install via <a href="https://www.nuget.org/packages/DepotDownloaderLib">nuget</a>: 

```cmd
PM> Install-Package DepotDownloaderLib
```

<h2>Overview:</h2>

The DepotDownloaderLib is a simple Wrapper Library for <a href="https://github.com/SteamRE/DepotDownloader">SteamRE/DepotDownloader</a> so u can interface with it easily inside ur Programm

<h3>Usage:</h3>
Start by creating a List to store the arguments you want to provied to DepotDownloader

```cs
List<DownloaderArgument> arguments = new List<DownloaderArgument>();
```

then you add your add your desired Arguments by adding objects of type "DownloaderArgument" to your list, these take 2 parameters (Argument Type and Argument Value), like in following Example.
Add the bottom of the ReadMe File you will find a list of all supported argument types.
The Following Example downloads a specific Manifest from R6S, so your account needs to own this game to be able to download this manifest

```cs
arguments.Add(new DownloaderArgument(ArgType.AppId, "359550"));
arguments.Add(new DownloaderArgument(ArgType.DepotId, "377237"));
arguments.Add(new DownloaderArgument(ArgType.ManifestId, "8358812283631269928"));
arguments.Add(new DownloaderArgument(ArgType.Username, "steamLoginName"));
arguments.Add(new DownloaderArgument(ArgType.Password, "steamPassword"));
arguments.Add(new DownloaderArgument(ArgType.Directory, @"C:\Users\username\Downloads\testfolder"));
```
<br>
To start the download with the arguments from the List, all you need to do is call the following method:

```cs
DepotDownloaderLib.StartDownload(arguments);
//If calling this method from a GUI, call this instead:
DepotDownloaderLib.StartDownload(arguments, true);
//this calls the method in a backgroundWorker instead so it doesnt block the UI thread
```

<h3>Extended Usage:</h3>

using DepotDownloaderLib.onConsoleOutput you can add ur own functionality to DepotDownloaders "BuiltIn" Console Output.
For example with the following code u can access the current download percentage and the latest written file path.

```cs
//f is the current download progress (type float)
//s is the latest written file (type string)
DepotDownloaderLib.onConsoleOutput += (f, s) =>
{
    Console.WriteLine("Current download progress: " + f);
    Console.WriteLine("Last written file " + s);
};
```

by default, DepotDownloader request the 2FA Code as a Console.ReadLine, you can intercept this call by using the following code:

```cs
DepotDownloaderLib.onConsoleInput += () =>
{
    return "Example2FACode";
};
//The return data of this function gets directly piped into the DepotDownloader 2FA Request instead of its default Console.ReadLine
```
This can be used to for example get the 2FA code from a UserInput inside the GUI of your app

<h3>Supported Argument Types:</h3>

```cs
public enum ArgType
{
    AppId,
    DepotId,
    ManifestId,
    Username,
    Password,
    RememberPassword,
    Directory,
    MaxServers,
    MaxDownloads,
}
```
