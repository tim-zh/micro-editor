# micro-editor

## usage

```html
<script src="javascripts/micro-editor.js"></script>
...
<div id="buttonsContainer"></div>
<textarea id="textHere"></textarea>
```

```javascript
microEditor(document.getElementById('textHere'), document.getElementById('buttonsContainer'));
```
or with options
```javascript
microEditor(document.getElementById('textHere'), document.getElementById('buttonsContainer'), {
	//tag that will be used to create buttons
	buttonElement: 'button',

	//default classes for buttons
	buttonClassName: 'microEditor-button',

	//default classes for button groups
	buttonGroupClassName: 'microEditor-buttonGroup',

	//list of button (provided and custom) names appended to buttonContainer.
	// | sign splits buttons into groups.
	//provided buttons use bbCode. preview button uses togglePreview() method added to text container
	buttons: 'bold,italic,underline,strike,size|link,image|quote,list,code|center,paragraph|preview' +
		//custom buttons, see below
		',hello1,hello2',

	//list of rule names that convert text to html to see in preview
	previewReplacements: 'newLine,bold,italic,underline,strike,size,link,link2,image,image2,quote,' +
		'list,code,center,paragraph',

	//custom buttons
	customButtons: {
		//button title string, startTag string, endTag string, class names string
		//this one when clicked wraps selected text in [h2]..[/h2]
		hello1: ['hi', '[h2]', '[/h2]', 'btn-default'],

		//the fourth is a special onclick handler
		hello2: ['hey', '', '', 'btn-primary', function(text, selectionStart, selectionEnd) {
			var name = prompt('type a name');
			//insertInString is the second method, shipped with microEditor()
			return 'hey, ' + insertInString(text, 'regards, ' + name, selectionEnd);
		}]
	},

	//additional rules to previewReplacements
	customReplacements: [
		[/\[h2\]([\s\S]+?)\[\/h2\]/g, '<h2>$1</h2>']
	],

	//function, called after preview was shown
	onPreview: function(previewContainer) {previewContainer.style.background = '#aff'}
});
```