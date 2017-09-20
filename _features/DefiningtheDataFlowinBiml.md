---
title: "BIML: Defining the Data Flow"
component: ssis
---
*This post is [part 5 of a series](http://agilebi.com/jwelch/2011/05/13/biml-functionality-in-bids-helper/) on using [Biml](http://www.varigence.com/documentation/biml/) in
{{site.title}}. This post builds on some of the information and the sample from the previous posts.*

In the previous post in the series, I talked about <a href="http://agilebi.com/jwelch/2011/06/13/controlling-the-control-flow-in-biml/">
controlling the order of execution in the control flow</a>. In this post, the focus will be on the dataflow, and controlling how the data in the pipeline flows from one component to the next. This post uses a new table as the target of the data flow, so you may want to review <a href="http://agilebi.com/jwelch/2011/05/26/creating-tables-using-biml-and-bimlscript/">
Part 2: Creating Tables using Biml and BimlScript</a> to see how to create the table locally. The Biml below describes the table. You can create it in the database of your choice - I used a database named Target.

<pre>&lt;Biml xmlns=&quot;http://schemas.varigence.com/biml.xsd&quot;&gt;
    &lt;Connections&gt;
        &lt;OleDbConnection Name=&quot;Source&quot; ConnectionString=&quot;Provider=SQLNCLI10;Server=.;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=SSPI;&quot;/&gt;
        &lt;OleDbConnection Name=&quot;Target&quot; ConnectionString=&quot;Provider=SQLNCLI10;Server=.;Initial Catalog=Target;Integrated Security=SSPI;&quot;/&gt;
    &lt;/Connections&gt;
    &lt;Tables&gt;
        &lt;Table Name=&quot;DimAccount_Test&quot; ConnectionName=&quot;Target&quot;&gt;
            &lt;Columns&gt;
                &lt;Column Name=&quot;AccountKey&quot; /&gt;
                &lt;Column Name=&quot;ParentAccountKey&quot; IsNullable=&quot;true&quot; /&gt;
                &lt;Column Name=&quot;AccountCodeAlternateKey&quot; IsNullable=&quot;true&quot; /&gt;
                &lt;Column Name=&quot;ParentAccountCodeAlternateKey&quot; IsNullable=&quot;true&quot; /&gt;
                &lt;Column Name=&quot;AccountDescription&quot; DataType=&quot;String&quot; Length=&quot;50&quot; IsNullable=&quot;true&quot; /&gt;
                &lt;Column Name=&quot;AccountType&quot; DataType=&quot;String&quot; Length=&quot;50&quot; IsNullable=&quot;true&quot; /&gt;
                &lt;Column Name=&quot;Operator&quot; DataType=&quot;String&quot; Length=&quot;50&quot; IsNullable=&quot;true&quot; /&gt;
                &lt;Column Name=&quot;CustomMembers&quot; DataType=&quot;String&quot; Length=&quot;300&quot; IsNullable=&quot;true&quot; /&gt;
                &lt;Column Name=&quot;ValueType&quot; DataType=&quot;String&quot; Length=&quot;50&quot; IsNullable=&quot;true&quot; /&gt;
                &lt;Column Name=&quot;CustomMemberOptions&quot; DataType=&quot;String&quot; Length=&quot;200&quot; IsNullable=&quot;true&quot; /&gt;
            &lt;/Columns&gt;
        &lt;/Table&gt;
    &lt;/Tables&gt;
&lt;/Biml&gt;</pre>

With the table created, we can move on to the interesting part &ndash; transforming the data. In a simple, straightforward data flow, the Biml compiler will do most of the work for you. Take this data flow as an example:

<pre>&lt;Dataflow Name=&quot;Dataflow 1&quot;&gt;
    &lt;Transformations&gt;
        &lt;OleDbSource Name=&quot;Source&quot; ConnectionName=&quot;Source&quot;&gt;
            &lt;DirectInput&gt;SELECT * FROM dbo.DimAccount&lt;/DirectInput&gt;
        &lt;/OleDbSource&gt;
        &lt;OleDbDestination Name=&quot;Target&quot; ConnectionName=&quot;Target&quot;&gt;
            &lt;ExternalTableOutput Table=&quot;dbo.DimAccount_Test&quot;/&gt;
        &lt;/OleDbDestination&gt;
    &lt;/Transformations&gt;
&lt;/Dataflow&gt;</pre>

In this case, you don&rsquo;t have to specify any data paths. The Biml compiler will infer that the OleDbSource's output should be connected to the input of the OleDbDestination.

![](Defining the Data Flow in Biml_image_2.png)

The compiler is able to do this by using default outputs. In Biml, most components have a default output defined. In the absence of other information, the compiler will automatically connect the default output of a transformation to the input of the next component defined in the Biml. So, if we use a slightly more complex data flow, like this:

<pre>&lt;Dataflow Name=&quot;Dataflow 2&quot;&gt;
    &lt;Transformations&gt;
        &lt;OleDbSource Name=&quot;Source&quot; ConnectionName=&quot;Source&quot;&gt;
            &lt;DirectInput&gt;SELECT * FROM dbo.DimAccount&lt;/DirectInput&gt;
        &lt;/OleDbSource&gt;
        &lt;Lookup Name=&quot;Check For Existing&quot; OleDbConnectionName=&quot;Target&quot; NoMatchBehavior=&quot;RedirectRowsToNoMatchOutput&quot;&gt;
            &lt;DirectInput&gt;SELECT AccountKey FROM dbo.DimAccount&lt;/DirectInput&gt;
            &lt;Inputs&gt;
                &lt;Column SourceColumn=&quot;AccountKey&quot; TargetColumn=&quot;AccountKey&quot;/&gt;
            &lt;/Inputs&gt;
        &lt;/Lookup&gt;
        &lt;ConditionalSplit Name=&quot;Test ID Range&quot;&gt;
            &lt;OutputPaths&gt;
                &lt;OutputPath Name=&quot;High ID&quot;&gt;
                    &lt;Expression&gt;AccountKey &gt;= 100&lt;/Expression&gt;
                &lt;/OutputPath&gt;
            &lt;/OutputPaths&gt;
        &lt;/ConditionalSplit&gt;
        &lt;OleDbDestination Name=&quot;Target&quot; ConnectionName=&quot;Target&quot;&gt;
            &lt;ExternalTableOutput Table=&quot;dbo.DimAccount_Test&quot;/&gt;
        &lt;/OleDbDestination&gt;
    &lt;/Transformations&gt;
&lt;/Dataflow&gt;</pre>

We end up with a data flow that still automatically connects data paths between components. In this case, though, it&rsquo;s probably not doing exactly what we want, since it&rsquo;s just connecting the default outputs. The Conditional Split ("Test ID Range") in this example is connected by the default output, but we want to use the "High ID" output to filter out IDs less than 100. In the case of the Lookup ("Check For Existing"), the default output being used is the "Match"  output, but we only want the non-matched records, so that only new rows are inserted.

![](Defining the Data Flow in Biml_image_6.png)

  *I explicitly choose the option BIDS to display the path Source Names for this screenshot &ndash; by default, they aren't displayed in the generated package. You can change the setting in BIDS by selecting the path, opening the Properties tool window, and changing the PathAnnotation property to SourceName.*

So how would we change the Biml to get the desired results? If we add an [InputPath](http://www.varigence.com/documentation/biml/biml_Varigence.Languages.Biml.Transformation.AstDataflowInputPathNode.html) element to the appropriate components, we can control which output is tied to the component's input. In this case, we need to add explicit InputPath instructions to the Conditional Split (that will reference the Lookup's NoMatch output) and to the OleDbDestination (which will reference the ConditionalSplit's High ID output).

<pre>&lt;Dataflow Name=&quot;Dataflow 3&quot;&gt;
    &lt;Transformations&gt;
        &lt;OleDbSource Name=&quot;Source&quot; ConnectionName=&quot;Source&quot;&gt;
            &lt;DirectInput&gt;SELECT * FROM dbo.DimAccount&lt;/DirectInput&gt;
        &lt;/OleDbSource&gt;
        &lt;Lookup Name=&quot;Check For Existing&quot; OleDbConnectionName=&quot;Target&quot; NoMatchBehavior=&quot;RedirectRowsToNoMatchOutput&quot;&gt;
            &lt;DirectInput&gt;SELECT AccountKey FROM dbo.DimAccount&lt;/DirectInput&gt;
            &lt;Inputs&gt;
                &lt;Column SourceColumn=&quot;AccountKey&quot; TargetColumn=&quot;AccountKey&quot;/&gt;
            &lt;/Inputs&gt;
        &lt;/Lookup&gt;
        &lt;ConditionalSplit Name=&quot;Test ID Range&quot;&gt;
            &lt;InputPath OutputPathName=&quot;Check For Existing.NoMatch&quot;/&gt;
            &lt;OutputPaths&gt;
                &lt;OutputPath Name=&quot;High ID&quot;&gt;
                    &lt;Expression&gt;AccountKey &gt;= 100&lt;/Expression&gt;
                &lt;/OutputPath&gt;
            &lt;/OutputPaths&gt;
        &lt;/ConditionalSplit&gt;
        &lt;OleDbDestination Name=&quot;Target&quot; ConnectionName=&quot;Target&quot;&gt;
            &lt;InputPath OutputPathName=&quot;Test ID Range.High ID&quot;/&gt;
            &lt;ExternalTableOutput Table=&quot;dbo.DimAccount_Test&quot;/&gt;
        &lt;/OleDbDestination&gt;
    &lt;/Transformations&gt;
&lt;/Dataflow&gt;</pre>

This gives you the following data flow.

![](Defining the Data Flow in Biml_image_8.png)

That's a few examples of controlling the data paths in a data flow. There are a few other bits of information that are important to know about data paths in the data flow.

- Most components have a default output named "Output", and a second output named "Error" for the error output (if the component supports errors).
- The Multicast component has no default output, so you always need to explicitly define the data path mapping from it to the next component.
- The Union All, Merge, and Merge Join components need to be explicitly mapped, since they support multiple inputs.
- The Slowly Changing Dimension (SCD) transformation has multiple outputs. The "New" output is the default. There are also outputs named "Unchanged", "FixedAttribute", "ChangingAttribute", "HistoricalAttribute", and "InferredMember". 
- The Percentage Sampling and Row Sampling transformations have two output named "Selected" (the default) and "Unselected".

The <a href="http://cid-71c6f14e3c205217.office.live.com/self.aspx/Public/BimlSamples/DataFlow.zip">
sample Biml for this post is on my SkyDrive</a>. Please download it and try it out with the
[latest release](/downloads) of *{{site.title}}*.