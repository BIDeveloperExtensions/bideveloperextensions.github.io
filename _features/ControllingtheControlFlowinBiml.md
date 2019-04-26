---
title: "BIML: Controlling the Control Flow"
component: ssis
---


**Note: Varigence has stopped providing Biml for BI Developer Extensions so these features are deprecated. Instead install [BimlExpress](https://www.varigence.com/BimlExpress).**

--------------------


*This post is [part 4 of a series](http://agilebi.com/jwelch/2011/05/13/biml-functionality-in-bids-helper/)
on using [Biml](http://www.varigence.com/documentation/biml/) in
{{site.title}}. This post builds on some of the information and the sample from the previous posts.*

So far, we&rsquo;ve looked at some relatively simple packages, in terms of their flow. In this post, we&rsquo;re going to look at how to handle more complex control flow in Biml.

One feature of Biml is the ConstraintMode property that&rsquo;s part of packages and containers. This property controls how precedence constraints are generated in the control flow. In the simple case, if you want all tasks to be run in sequence, you can
 set the ConstraintMode to Linear. This causes the package to be produced with all tasks connected sequentially by Success precedence constraints, in the order they were specified in the Biml. So, the following Biml:

``` xml
<Biml xmlns="http://schemas.varigence.com/biml.xsd">
    <Packages>
        <Package Name="Control Flow Sample 1" AutoCreateConfigurationsType="None" ConstraintMode="Linear">
            <Tasks>
                <Dataflow Name="Task 1"/>
                <Dataflow Name="Task 2"/>
                <Dataflow Name="Task 3"/>
            </Tasks>
        </Package>
    </Packages>
</Biml>
```

This results in a package that looks like this:

![](Controlling the Control Flow in Biml_image_2.png)

This type of linear flow is great in some situations, but sometimes you need more control. In those cases, you can change the ConstraintMode to Parallel. The generated package will not have any automatically created precedence constraints, so it will look like this:

![](Controlling the Control Flow in Biml_image_4.png)

Once a container is in Parallel constraint mode, you can start adding explicit precedence constraints. Let&rsquo;s use an example to highlight this. Imagine you have a package that needs to run three data flows. (I'm using data flows for the example  because they are simple to read in Biml, and I want the focus to be on the constraints, not the tasks.) I want one data flow to execute first - this data flow will be named "Me First". If "Me First" succeeds, the data flow named
 "Me Next (Success)" should execute. The third data flow, named "I'm Last (Always)" should always be executed, regardless of the success or failure of the other two tasks. So my package should look like this:

 ![](Controlling the Control Flow in Biml_image_6.png)


So how do we get this output from Biml? We can use the [PrecedenceConstraints](http://www.varigence.com/documentation/biml/biml_Varigence.Languages.Biml.Task.AstTaskflowPrecedenceConstraintsNode.html) collection on each task. At it's simplest, you just add an [Input](http://www.varigence.com/documentation/biml/biml_Varigence.Languages.Biml.Task.AstTaskflowInputPathNode.html) to the collection, and reference the output of the task that should execute prior to this one. In Biml, all tasks have a built-in output named Output. You can reference it using TaskName.Output ("Me First.Output" in the example below).

This will create a regular, Success constraint between the tasks.

<pre>&lt;Dataflow Name=&quot;Me Next (Success)&quot;&gt;
    &lt;PrecedenceConstraints&gt;
        &lt;Inputs&gt;
            &lt;Input OutputPathName=&quot;Me First.Output&quot;/&gt;
        &lt;/Inputs&gt;
    &lt;/PrecedenceConstraints&gt;
&lt;/Dataflow&gt;</pre>

For the next set of constraints, we want to use the OR logical type, using the LogicalType property, for the constraints, since either of them should cause the third task to run. We also need to explicitly set the evaluation value on these, using the EvaluationValue property.

<pre>&lt;Dataflow Name=&quot;I'm Last (Always)&quot;&gt;
    &lt;PrecedenceConstraints LogicalType=&quot;Or&quot;&gt;
        &lt;Inputs&gt;
            &lt;Input OutputPathName=&quot;Me First.Output&quot; EvaluationValue=&quot;Failure&quot;/&gt;
            &lt;Input OutputPathName=&quot;Me Next (Success).Output&quot; EvaluationValue=&quot;Completion&quot;/&gt;
        &lt;/Inputs&gt;
    &lt;/PrecedenceConstraints&gt;
&lt;/Dataflow&gt;</pre>

You can also add expression constraints to the Inputs, to control whether tasks run based on the results on an expression. You use the EvaluationOperation and Expression properties to configure that.

<pre>&lt;Package Name=&quot;Control Flow Sample 3&quot; AutoCreateConfigurationsType=&quot;None&quot; ConstraintMode=&quot;Parallel&quot;&gt;
    &lt;Variables&gt;
        &lt;Variable Name=&quot;Continue&quot; DataType=&quot;Int32&quot;&gt;0&lt;/Variable&gt;
    &lt;/Variables&gt;
    &lt;Tasks&gt;
        &lt;Dataflow Name=&quot;Task 1&quot;/&gt;
        &lt;Dataflow Name=&quot;Task 2&quot;&gt;
            &lt;PrecedenceConstraints&gt;
                &lt;Inputs&gt;
                    &lt;Input OutputPathName=&quot;Task 1.Output&quot; EvaluationOperation=&quot;Expression&quot; Expression=&quot;@Continue==1&quot;/&gt;
                &lt;/Inputs&gt;
            &lt;/PrecedenceConstraints&gt;
        &lt;/Dataflow&gt;
    &lt;/Tasks&gt;
&lt;/Package&gt;</pre>

That Biml results in a package that looks like this.

 ![](Controlling the Control Flow in Biml_image_8.png)

That's how to control the precedence constraints. I've uploaded the Biml from this post to [my SkyDrive here](http://cid-71c6f14e3c205217.office.live.com/self.aspx/Public/BimlSamples/ControlFlow.biml), so you can download and experiment with this yourself. In the next post, we&rsquo;ll look at controlling the data paths in a data flow.

\[cross-posted from [http://agilebi.com/jwelch/2011/06/13/controlling-the-control-flow-in-biml/](http://agilebi.com/jwelch/2011/06/13/controlling-the-control-flow-in-biml/)]
