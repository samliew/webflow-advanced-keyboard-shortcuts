# Webflow Advanced Keyboard Shortcuts

Additional keyboard shortcuts for webflow.com designer interface

## Available shortcuts

* Shift + Alt : Edit "class" for selected element
* Enter : Edit the text in the selected element
* Shift + F : Quick access to font size
* Shift + Arrow Up / Down / Left / Right : Quick access to padding increase/decrease

## How to setup?

![gif](https://github.com/maciejsaw/webflow-advanced-keyboard-shortcuts/raw/master/keyboard%20webflow.gif)

1) Open your browser developer tools

2) Go to the console tab

3) Paste the following code into the console and press enter

```javascript
var WebflowAdvancedKeyboardShortcuts = (function() {
    var version = "1.1";

    // After clicking Esc on keyboard, the iframe is in focus so we need to bind the keys 
    // for both "documents": parent document and site iframe. 
    var $iframe = $(document).find('#site-iframe').contents();
    var $iframeDocument = $($iframe[0]); //this gets the document object of the iframe
    var $bothDocuments = $(document).add($iframeDocument);

    function clickInStyleTab(selector) {
        $('.style-tab').click();
        
        // slight delay needed to allow right panel tab to switch
        setTimeout(function() {
            $(selector).click();
        }, 50);
    }

    function focusInStyleTab(selector) {
        $('.style-tab').click();
        
        // slight delay needed to allow right panel tab to switch
        setTimeout(function() {
            $(selector).focus();
        }, 50);
    }

    function bindKeydownForClassInput() {
        $bothDocuments.bind('keydown', 'shift+alt', function() {
            clickInStyleTab('.token.add, .need-class');
        });
    }

    function bindEnterKey() {
        $bothDocuments.bind('keydown', 'return', function() {
            $iframe.find('.wf-selected').dblclick();
        });
    }

    function bindFontSize() {
        $bothDocuments.bind('keyup', 'shift+f', function() {
            focusInStyleTab('.font-size.pull-left  .kit-unit-box.kit-text-input .input');
        });
    }

    function bindPadding() {
        $bothDocuments.bind('keyup', 'shift+up', function() {
            clickInStyleTab('.padding .label.top');
        });
        $bothDocuments.bind('keyup', 'shift+down', function() {
            clickInStyleTab('.padding .label.bottom');
        });
        $bothDocuments.bind('keyup', 'shift+left', function() {
            clickInStyleTab('.padding .label.left');
        });
        $bothDocuments.bind('keyup', 'shift+right', function() {
            clickInStyleTab('.padding .label.right');
        });
    }

    function init() {
        $.getScript("https://cdn.rawgit.com/jeresig/jquery.hotkeys/master/jquery.hotkeys.js", function() {
            console.log('jQuery Hotkeys v'+version+' loaded.');
            bindKeydownForClassInput();
            bindEnterKey();
            bindPadding();
            bindFontSize();
        });
    }

    return {
        version: version,
        init: init,
    }

})();

WebflowAdvancedKeyboardShortcuts.init();

```

4) Enjoy your advanced keyboard shortcuts

Note: You need to run the above script each time you reload the page Webflow designer interface, but you don't need to remember the code. You can simply hit the arrow up to reuse the last command, or you can also save this as a snippet in Chrome "Sources" tab - right click in the Snippets sub-tab and select "New".

## How to use shortcuts?

* Shift + Alt --> Simply click [Shift] + [Alt] to focus the class selector. This is useful when adding classes to newly-placed elements.

![gif2](https://raw.githubusercontent.com/maciejsaw/webflow-advanced-keyboard-shortcuts/master/keyboard%20webflow2.gif)

* Text editing with "Enter" key and "Esc" --> When a text element is selected, it will enter text editing mode. Use [Esc] to leave
* Shift + F --> It will open font size increment window. Use [Up/Down] arrow keys to increase or decrease the font size, then use [Esc] when you're done
* Shift + Arrow Up / Down / Left / Right --> Opens a window to nudge respective padding: top, right, bottom or left. For example, use [Shift] + [Down] and then use [Up/Down] keys to increment padding-down by 1px. Hit [Enter] or [Esc] when you're done.

## Additional info

* This snippet uses the [jQuery Hotkeys](https://github.com/jeresig/jquery.hotkeys) library 
* More keyboard shortcuts will be added in the future, so check back for updates!

## See also

* [Webflow built-in keyboard shortcuts](https://help.webflow.com/article/does-the-webflow-designer-have-any-keyboard-shortcuts)
