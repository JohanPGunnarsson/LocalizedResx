
Sample demo project (verified on VS2013U) showing how to set up a WPF project for localization, using .resx files and satelite assemblies.  

Note that this line has been added to the project file (open as text), under the first section: (already done in project)

  <UICulture>sv-SE</UICulture>  

And in AssemblyInfo.cs this line has been added:

  [assembly: NeutralResourcesLanguage(“sv-SE", UltimateResourceFallbackLocation.Satellite)]

To rebuild only the satelite assembly, run resgen.exe and al.exe (Visual Studio Tools) with the following parameters (verified):

  resgen.exe /compile Strings.en-US.resx,LocalizedResx.Strings.en-US.resources 
  al.exe /t:lib /embed:LocalizedResx.Strings.en-US.resources /culture:"en-US" /out:"LocalizedResx.resources.dll”

Also worth to note, is how to run those commands to tag all controls in the WPF .xaml files with unique ids. 

After every edit of the XAML (already done in project):

  Msbuild /t:updateuid LocalizedResx.csproj  // generate Uid (**)

On every edit of the file, to discover modifications:

  Msbuild /t:checkuid LocalizedResx.csproj  // check Uid

Good luck! Let me know of any glitches. 
