# Custom HTML and JS in Qualtrics 

In a lot of the surveys I’ve worked on I've needed to include custom HTML and JavaScript so I’ve just included some of the stuff that I have learned along the way, from the basics to some slightly more complicated tricks.

## Adding Custom HTML 
When you click to edit the question text for a question that you want to edit you should see the interface below. 

{{:wiki:research:userstudies:prolific:add_html.png?600|}}

In the top left hand side of the interface, there is a tab that says “HTML View.” If you click on that tab you can start writing your HTML. If you try writing <b>bold text</b> in normal View you will see “<b>bold text</b>” whereas if you write the exact same thing in HTML View you will see “**bold text**.” The HTML view for the question is shown below. 

{{:wiki:research:userstudies:prolific:html_interface.png?600|}}

<u> Limitations </u>

It is worth mentioning that this is not a full HTML document. Think of this as only being a part of the body of the document. This means that you can’t include head tags or anything like that. You can **NOT** include javascript in the HTML you write here. This means no script tags, no onclick functions, etc. We will go into more depth on how to include JS later in this guide. **You should always store a backup of your custom HTML somewhere other than in Qulatrics.** It can be very easy to delete all of your div tags and other HTML if you accidentally **modify** anything while in "Normal View."


<u>Previewing Your Question</u>

You may notice that when you click out of the question you are adding HTML to that it doesn’t look at all how you would expect it to. This is no reason to panic! When you are clicking on the question to the right of the survey you will see a bar of options to the right of the question. This is where you usually select the type of question, the number of options, validation options, etc. There will also be a section called “Actions” that is shown below. Clicking on “Preview Question” will pull up a screen that will show you how your question will look (in a browser) to a person taking your survey. If it doesn’t look right here you probably need to do some more work with custom styling (which there is more information about later in this guide). You can also just take the survey as if you were a participant. In the new survey flow, you can click on the “…” in the upper hand corner of the question and click “Preview Question.” 




## Including JavaScript 

As was mentioned in the previous edition you cannot put any of your JavaScript directly into your HTML, there are specific places that you can include it.

The first place that you can add JS directly to a question. With the old interface, you can click on the gear to the left of the question and click “Add JavaScript…”

Once you click on this screen you will see the following code block
<code>
Qualtrics.SurveyEngine.addOnload(function()
{
	/*Place your JavaScript here to run when the page loads*/

});

Qualtrics.SurveyEngine.addOnReady(function()
{
	/*Place your JavaScript here to run when the page is fully displayed*/

});

Qualtrics.SurveyEngine.addOnUnload(function()
{
	/*Place your JavaScript here to run when the page is unloaded*/

});
</code>

The comments tell you when each of the functions will run. I usually put my code into the addOnReady function. 

In the old interface, once you have added JS to a question a black square that says JS will show up under the gear. Clicking on this will get you back to the javascript quickly.


Since you can’t just directly add JavaScript to your HTML if you want functions to run when some event happens you can use event listeners. I included some examples below. Usually, this just means that you should add ids to your HTML elements so you can more easily add your event listeners later on. In general, you need to write out “jQuery” instead of using “$”.

<code>
document.getElementById("id1").addEventListener("click", function(){ your js code here });
document.getElementById("id2").addEventListener("change", function(){ your js code here });


</code>

## Useful Qualtrics JS Commands

*Read Embedded Data*
<code>var <js variable_name> = Qualtrics.SurveyEngine.getEmbeddedData('<embedded data variable name>');
</code>

*Setting Embedded Data*
<code>
Qualtrics.SurveyEngine.setEmbeddedData("<embedded_data_variable_name>", <value to set>);
</code>

This can be very useful if you want to do branching logic in the survey flow based on a decision you make using javascript. It is also a way to save information that you derive with JS along with the participant’s other responses.

*Using JS to select/deselect an option in a question*
<code>var err_occured = this.setChoiceValue(<index>, <true or false>);</code>
Note: The index does not refer to the index that the option appears in the list of options. To determine the index of the option you want to select/deselect try using Piped Text to display the option the last number inside of the curly brackets is the index you want to use.


*Hide a question*
<code>jQuery(“#”+this.questionId).hide();</code>

*Hide next button*
<code>
Qualtrics.SurveyEngine.addOnReady(function () {
$('NextButton').hide();
});
</code>

Hiding a question combined with using JS to select/deselect options is a good way of only presenting a user with specific options based on JavaScript.


==== External JavaScript ====
There are several ways to include external scripts putting this into the javascript for a question is one way of doing it. There also seem to be ways of including an external JavaScript file so that it can be used for any/all of the questions in your survey, but I have not been able to get it to work.
<code>
jQuery.getScript( “<url to script>",function(){
	/* your JavaScript code here */	
	});
</code>



insert this into the js for the question
<code>
document.getElementById("[insert html id here]").innerHTML = Qualtrics.SurveyEngine.getEmbeddedData("<embedded_data_variable_name>");
</code>


insert this into html view of question
<code>
	<span id="[insert html id here]"></span>
</code>


<u>Testing</u>

You can test your JS in the same way you check your HTML (using preview or taking the survey). Be warned, if your JS depends on a URL parameter it will not be set if you are just testing it in a preview.





## Including CSS 

If you want to include CSS for your project there are multiple ways that you can do it.
  - You can add the CSS directly to the custom HTML with the style attribute
  - You can add custom CSS to the whole survey
  - You can add an external custom CSS file to the whole survey

For options 2 and 3 go to the “Look and Feel” tab. In that tab click on “Style” and scroll down. You can paste your custom CSS directly into the “Custom CSS” text box or add a link to your external CSS file hosted elsewhere.

It is worth noting that Qualtrics has its own built-in style sheet. By default, it does things like hiding custom radio and checkboxes. In my own experience, the way to make those custom elements show up again is to add the style attribute directly to the element that is being hidden by Qualtrics (putting it in the Custom CSS block didn’t work for me). The code snippet below shows the style attribute that I use to show hidden radio buttons. In my case, I also had to add the “position:relative” attribute to the element that was next to my radio button so they wouldn’t overlap.

<code>style="display: visible; opacity: 100; position:relative;"</code>


# TODO
- validate matrix
- can't use format strings!!!!!
- iframes
