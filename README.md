<div align="center">

## Don't trust Int


</div>

### Description

The Int function can return incorrect results. Don't use it directly, but instead wrap it in your own function to make the problems disappear.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Mel Grubb II](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/mel-grubb-ii.md)
**Level**          |Beginner
**User Rating**    |4.2 (25 globes from 6 users)
**Compatibility**  |VB 6\.0
**Category**       |[VB function enhancement](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/vb-function-enhancement__1-25.md)
**World**          |[Visual Basic](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/visual-basic.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/mel-grubb-ii-don-t-trust-int__1-22005/archive/master.zip)





### Source Code

<br><b>Update:</b><br>
Already since submitting the article (About an hour ago), there has been a lot of feedback and we've collectively found the following things:<br><br>
1) The problem only appears in the IDE.<br><br>
2) The FIRST time you use Int in the IDE, it works correctly. Subsequent calls return incorrect results.<br><br>
Thanks to Sean Street for his feedback.<br>
I'm going to clear out some of the comments to lessen the confusion now that we seem to have a better grip on the problem.<br><br>
<b>Original Article Follows:</b><br><br>
<b>Problem:</b><br>While tracing through some game code the other day, I noticed a wrong number. I very carefully evaluated every part of the statement, and discovered that the bug lay within the Int function itself. You can reproduce this in the immediate window in one line.
<br><br>
Go to the Immediate (Debug) window and type the following:<br>
? Int(0.7 * 10)<br><br>
It will say 6. EXCUSE ME? The integer of 7 is six? If you put 7 in the parenthesis, you will get the answer 7. It is only when you pass a calculation into the function that the results come back wrong.<br><br>
The truly amazing part is that Microsoft has alrady found and fixed this bug once before. Way back in version 4. Check out this KB article:<br>
<A href="http://support.microsoft.com/support/kb/articles/Q138/5/22.asp">http://support.microsoft.com/support/kb/articles/Q138/5/22.asp</A><br><br>
<b>Solution:</b><br>
Well, I guess we wait for Microsoft to fix it AGAIN, but in the meantime we can write a function to "wrap" the int function so that you are not passing it a calculation any more. I've called mine mInt for "Make Integer" because CInt is already taken (And by the way, behaves differently as I'll describe below).<br><br>
Public Function mInt(ByVal Value As Double) As Integer<br>
  mInt = Int(Value)<br>
End Function<br><br>
By passing the calculation into this function, we are forcing it to evaluate down into a single variable (Value). This seems to eliminate the problem.<br><br>
As I said above you can't just use CInt instead of Int because they act differently. In immediate mode type the following:<br>
? CInt(4.5)<br><br>
You get 4, right? Now type:<br>
? CInt(4.6)<br><br>
You get 5. CInt rounds numbers when converting them, so it's useless for replacing Int which simply truncates the fractional portion of a number.<br><br>
<B>Rant:</b><br>This sort of bug is simply unacceptable. To get incorrect results from one of the basic, fundamental building blocks of a language calls the reliability of the whole language into question.<br><br>
Get this, Microsoft doesn't even PRETEND that they are going to acknowledge your bug report any more. Most companies respond to bug reports, but M$ doesn't even have a spot on the form to put your email address any more. This guarantees that you'll never get so much as a "Thank you" from the evil empire. I can also pretty much guarantee that you won't see this bug acknowledged on the website until it has been fixed.<br><br>
MG2

