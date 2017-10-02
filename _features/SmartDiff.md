---
title: Smart Diff
category:
component: 
    - ssis
    - ssasm
    - ssast
    - ssrs
compatibilitylevel: 1103
---
_Note:_ You must have either [Microsoft Visual SourceSafe 2005](http://msdn2.microsoft.com/en-us/vstudio/aa718670.aspx) or Microsoft Visual Studio Team Explorer [2005](http://www.microsoft.com/en-us/download/details.aspx?id=7203)/[2008](http://www.microsoft.com/en-us/download/details.aspx?id=16338)/[2010](https://blogs.msdn.microsoft.com/jasonba/2010/02/11/team-explorer-is-included-in-visual-studio-2010/) (described [here](http://www.codeplex.com/CodePlex/Wiki/View.aspx?title=Obtaining%20the%20Team%20Explorer%20Client)) installed as *{{site.title}}* leverages the visual diff dialog from either of those tools. (Though at least one of those tools must be installed, your solution does not need to be bound to source control to utilize Smart Diff.) Visual Studio 2012+ includes a built-in diff viewer, so *{{site.title}}* (starting with version 1.6.5) will leverage it.

_Note:_  Starting in release 1.4.2.2, you can setup a custom command line diff viewer in the [Preferences](../Preferences) screen. Once setup, you do not need to have VSS or TFS installed to use Smart Diff.

The **{{site.title}}** Smart Diff feature lets you compare versions of a SSAS, SSIS, and SSRS files. 
**{{site.title}}** preprocesses XML files so that the diff versus source control is more meaningful.

Doing a diff on two versions of an Integration Services package is very unhelpful because the XML of the dtsx file is not formatted in a way that lends itself to comparison.  The XML is not pretty-printed, the XML elements aren't always in the same order even when order isn't important, and unnecessary information about layout and formatting obscures detecting differences which actually impact execution of the package.

The Smart Diff feature pre-processes the files by pretty-printing the XML, ordering elements in a consistent manner, and removing unnecessary layout/formatting information. Smart Diff supports comparing to versions from Microsoft Visual SourceSafe and Microsoft Team Foundation Server. Smart Diff can also be run to compare two files on the local disk when the current solution is not bound to source control (or if it is bound to an unsupported source control).

**Without {{site.title}}**

![](Smart Diff_SmartDiffOutOfTheBox.png)

**With {{site.title}}**

![](Smart Diff_SmartDiffVisualDiff.png)

Reporting Services report provide a similar problem in that the order of some tags is not important, but they make a diff unusable. For instance, in the following screenshot, note that despite the difference in ordering of tags, nothing has really changed:

![](Smart Diff_SmartDiffSSRSBefore.png)

Right-clicking on the file in Solution Explorer lets you launch the Smart Diff feature:
![](Smart Diff_SmartDiffMenu.png)

![](Smart Diff_SmartDiffOptions.png)

**Other Source Control Systems**
If you would like Smart Diff to support other source control systems please create an issue [here](/issues) requesting that.

If you use TortoiseSVN, see the [ORAYLIS BI.SmartDiff](http://bismartdiff.codeplex.com) CodePlex project for an alternative.
