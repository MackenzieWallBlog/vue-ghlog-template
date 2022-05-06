When you come to review a merge request, there are a lot of things to check for, and it is difficult to keep them in your working memory all at the
same time.

These are also great ways to double check your own work before submitting your MR for others to review.

## The Prompt Lens
Does this actually address the ticket? There are plenty of times a ticket is misunderstood, it is great to get a double check. 
The more info you have, the better your review will be.

## The Architecture Lens
Take a step back: Would you approach this problem differently at the highest level? Does the data flow make sense? Will updates have expected
behavior? Is there a synchronous call to redux for something that may need updates? What are the inputs and outputs? When will it change?
*Extra Credit: If it is a big change that is hard to grok in the gitlab web client, pull down the branch and click around and see how it is working
yourself! Add a couple debug statements or console.logs

## The Learning Lens
Is there something either of you could learn from this MR? Maybe you haven't used this technology before, or something seems missing the writer
doesn't know about. This is a great time to discuss and disseminate knowledge- explaining something in your own words is a great way to solidify
your knowledge- this helps everyone!
##The Habitat Lens
Is this the right place for this code to be? Maybe this new effect, redux value, etc, is really the concern of another part of the app.

## The Performance Lens
Is there a more efficient way to do this? Every spare cycle counts on console! Take a close peek for memory leaks. Every subscription should be
cleaned up. Maybe there is a loop that could be optimized to return early. Have you chained loops so that you're iterating over an array multiple
times whereas you could do it in one iteration? Are you calling functions in a template for a value that never changes once initialized properly.
Maybe a search or filter could reduce cycles.
Many times, the first way we solve the problem is not the more efficient, and this is when to catch.
Example of increasing performance by reducing redraws:
this.unreadRequestsReceived = this.store.getValue().friend2.unreadRequestsReceivedCount; // This
synchronously gets the current state's value, reducing the minimum number of draws from 2 to 1 by getting the
current value in ngOnInit before the first draw
```this.unreadRequestsReceivedCount$.pipe(
distinctUntilChanged(), // Reducing redraws can be done with a pipe
takeUntil(this.onDestroy$)
).subscribe((unreadRequestsReceivedCount) => {
if (this.showingUnreadCount && this.unreadRequestsReceived === unreadRequestsReceivedCount) { return;
} // Or, in the handler, if there is more logic you need to do to determine if a redraw should occur or not
this.unreadRequestsReceived = unreadRequestsReceivedCount;
this.cdr.markForCheck();
});
```

## The Tribal Knowledge Lens
If a new teammate without your knowledge joined our team and tried to understand this code, would it be easy? Maybe it needs clearer names or a
comment explaining the intent. If you don't know how something works, ask! Just trying to explain it can help write the comment or name that
makes the purpose clear.

## The Style Lens
This is where whitespace, naming, missing semi-colons come up.

## Debug Code Cleanup Lens
Was this code added to test something? Hardcoded values, debug statements, console.logs- sometimes the author becomes blind to these
statements accidentally commits them. One good tip is tagging your console logs with something easy to search that will jump out at the reviewer.
It is especially easy to leave these in the html. This one trips me up the most! :)

##The Adversarial Lens
Pretend for a moment it is your coworkers mission to put a memory leak into the code and break the program. Sometimes too much team trust can
let memory leaks or other issues sneak past a code review. Team trust is great- outside of the code review process.
The Test Lens
Are there unit tests? Well, maybe there should be!
