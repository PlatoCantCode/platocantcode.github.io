#### *ctrl-e in obsidian will show preview mode* 
****
#### Font Basics
Double space for new line
Return key for soft break

****

*italics*
**bold**
***Both***

****

##### Block quote
> block quote
ensure each line gets it 




create a 2 line space break to escape the block quote.


escape symbol is \ 
****
#### Basic List
* heading 1 
	* sub heading 2
		* sub heading 3
		* 1918\. was a good year - notice the escape to prevent it from becoming a numbered list.
			* to use an actual number, you might need the escape char
*****
#### Numbered list
The numbers don't matter, mark down will order correctly.
1. item 1
4. item 2
	1. sub number
		1. 3rd tier number
7. just like normal really
8. Except the numbers don't matter and it'll auto sort it for you! Which is **GREAT**

****
#### Code Blocks
use the \`  symbol

` this is an example block`

Encase the code with  2 backticks if you need a quote within the code
``this is my command with its own `backtick` ``

To state what code exactly use three \`\`\` and type code type and end with \`\`\`

```powershell
update-help
```

```powershell
get-command help -verbose
```

****

#### Lines
\**** = create a line 

*****

#### Quick Create Link
use < > around the url or email to just make it a link. But you might need to use the https:// at the start to get it to recognize it properly in Obsidian.
<https://www.google.com>


****

#### Inline  Links:
 First brackets then parenthesis
 No space between the two items
[link title](www.url.com)


Reference Links:
Reference links don't appear in the rendered Markdown. 
They are defined by tag brackets with tag -> : then url

In the main text block - use a a pair of [ ] [ ] 
First [ ] is for display text
Second [ ] is for the tag

Link the definition to the url 
(Place at end of document for easy link modification)
*note that there is bracket : then space url*
[tag ]: url

###### Example:
All buildings are [taller then everything else][link1]
this is the rest of my paragraph. and the text keeps going on and on and on. Until I need to prove that [new york city][link2] has the most tall buildings and its the tallest...but also i can keep the link names in line like this. Be sure to check out [google][google.com] for reference! Oh, and I can reuse the links like this. The building link again is [here it is again][link1]. Just in case you needed to get to the tall building source.

Links: The value of this is that I can just change the link here 
[link1]: www.tallbuildings.com
[link2]: www.nyc.gov
[google.com]: www.google.com


****
# Headers with a \#
# Header one #
## Header two ##
### Header three ###
#### Header four ####
##### Header five #####
###### Header six ######

(try to stick with header 2 or 4)
Header 1 = largest
Header 6 = smallest

****
