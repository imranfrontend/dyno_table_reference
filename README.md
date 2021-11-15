dynoTable: A JQuery plugin for creating editable tables
A while back I was working on a project that required the GUI to allow the user to dynamically add, remove and rearrange various form fields contained in table rows. The tricky part was that the UI needed to have this functionality for several different types of elements across several different forms. For instance, one set of fields was for adding and removing specifications to a product while another set of fields was for adding images to a product. Thus, I needed a solution that would be flexible enough to work across virtually any type of form elements.

Naturally, I turned to JQuery. I first took a look around within JQuery’s plugin ecosystem to see if perhaps there was already a plugin that might do the job. While I did find a few different plugins for adding removing form elements, none of them did exactly what I needed, specifically re-arranging items… So, I was left with either trying to hack the functionality into an existing plugin, or roll up my sleeves and write my own. I choose the later option, since JQuery’s excellent extension mechanism makes writing plugins a fairly straightforward process. The result is the plugin below, which I call dynoTable.

What the plugin does
DynoTable makes an html table editable. With it you can:

Add rows
Remove rows
Clone rows
Click and Drag to Re-arrange rows (If you have Jquery UI included on your page)
Getting started with dynoTable is a snap. First make sure you have JQuery, and the dynoTable plugin, included in your page like so:


<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
<script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jqueryui/1.8.18/jquery-ui.min.js"></script>
<script type="text/javascript" src="jquery.dynotable.js"></script>
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
<script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jqueryui/1.8.18/jquery-ui.min.js"></script>
<script type="text/javascript" src="jquery.dynotable.js"></script>
Next, once the dom has loaded, simply instantiate dynoTable like so:

$(document).ready(function(){
    $('#t1').dynoTable();
});
$(document).ready(function(){
    $('#t1').dynoTable();
});
Given an html table similar to the one below, you will have the ability to add rows, clone rows, remove rows, and rearrange rows (rearranging works only if you have included JQuery UI)

<table id="t1" class="example">
    <tr id="add-template">
        <td>
            <img class="drag-handle" src="drag.png" alt="click and drag to rearrange" />
        </td>
        <td>
            <input id="tf1" type="text" value="I am in a table row!" /> 
        </td>
        <td>
            <select>
                <option>Yes</option>
                <option>No</option>
                <option>Unsure</option>
            </select>
        </td>
        <td>
            <img class="row-cloner" src="clone.png" alt="Clone Row" />                        
        </td>
        <td>
            <img class="row-remover" src="remove.png" alt="Remove Row" />
        </td>
    </tr>
</table>

<table id="t1" class="example">
    <tr id="add-template">
        <td>
            <img class="drag-handle" src="drag.png" alt="click and drag to rearrange" />
        </td>
        <td>
            <input id="tf1" type="text" value="I am in a table row!" /> 
        </td>
        <td>
            <select>
                <option>Yes</option>
                <option>No</option>
                <option>Unsure</option>
            </select>
        </td>
        <td>
            <img class="row-cloner" src="clone.png" alt="Clone Row" />                        
        </td>
        <td>
            <img class="row-remover" src="remove.png" alt="Remove Row" />
        </td>
    </tr>
</table>
Looking at the table above, you’ll notice a few classes:

row-cloner – clones the row when clicked
row-remover – removed the row when clicked
drag-handle – click and drag to rearrange row
And ids:

add-row – when clicked adds a row to the table
add-template – the table row template used when add-row is clicked.
This row is NOT visible, it is only used as a template for rows that are added.
These specify what the user can click on to interact with the table. The result of which is below:

Note: You can change these class-names to anything you want by passing in them as properties to dynoTable. See available properties.

Example (Click Add Row to add a table row)

Configuring dynoTable
The dynoTable defaults will probably handle most use cases. If you do not require any of the functionality it provides, you can simply omit the classes from your table. However, dynoTable also provides a number of properties and callback functions to configure it further if needed.

To pass configuration options and callback functions to dynoTable, you simply pass them in as an object, when instantiating the plugin. For example:

/*
 * dynoTable configuration options
 * These are the options that are available with their default values
 */
$('#myTable').dynoTable({
    removeClass: '.row-remover',        //class for the clickable row remover
    cloneClass: '.row-cloner',          //class for the clickable row cloner
    addRowTemplateId: '#add-template',  //id for the "add row template" 
    addRowButtonId: '#add-row',         //id for the clickable add row button, link, etc
    lastRowRemovable: true,             //If true, ALL rows in the table can be removed, otherwise there will always be at least one row
    orderable: true,                    //If true, table rows can be rearranged
    dragHandleClass: ".drag-handle",    //class for the click and draggable drag handle
    insertFadeSpeed: "slow",            //Fade in speed when row is added
    removeFadeSpeed: "fast",            //Fade in speed when row is removed
    hideTableOnEmpty: true,             //If true, table is completely hidden when empty
    onRowRemove: function(){
        //Do something when a row is removed
    },
    onRowClone: function(){
        //Do something when a row is cloned
    },
    onRowAdd: function(){
        //Do something when a row is added
    },
    onTableEmpty: function(){
        //Do something when ALL rows have been removed
    },
    onRowReorder: function(){
        //Do something when table rows have been rearranged
    }
});

/*
 * dynoTable configuration options
 * These are the options that are available with their default values
 */
$('#myTable').dynoTable({
    removeClass: '.row-remover',        //class for the clickable row remover
    cloneClass: '.row-cloner',          //class for the clickable row cloner
    addRowTemplateId: '#add-template',  //id for the "add row template" 
    addRowButtonId: '#add-row',         //id for the clickable add row button, link, etc
    lastRowRemovable: true,             //If true, ALL rows in the table can be removed, otherwise there will always be at least one row
    orderable: true,                    //If true, table rows can be rearranged
    dragHandleClass: ".drag-handle",    //class for the click and draggable drag handle
    insertFadeSpeed: "slow",            //Fade in speed when row is added
    removeFadeSpeed: "fast",            //Fade in speed when row is removed
    hideTableOnEmpty: true,             //If true, table is completely hidden when empty
    onRowRemove: function(){
        //Do something when a row is removed
    },
    onRowClone: function(){
        //Do something when a row is cloned
    },
    onRowAdd: function(){
        //Do something when a row is added
    },
    onTableEmpty: function(){
        //Do something when ALL rows have been removed
    },
    onRowReorder: function(){
        //Do something when table rows have been rearranged
    }
});
Callbacks: Extending dynoTable
In addition to the configuration options, you can pass in your own behaviors as call back functions, as shown above. The available callbacks are:

onRowRemove – Called when a row is removed
onRowClone – Called when a row is cloned
onRowAdd – Called when a new row is added
onTableEmpty – Called when ALL rows have been removed
onRowReorder – Called when rows have been rearranged by the user
The example below shows an example of how dynoTable might be used in conjuntion with callback functions. When you add, clone, or rearrange the beers in the table, their numbers update automagically.

Example Code
<!DOCTYPE html>
<html>
    <head>
        <title></title>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
        <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jqueryui/1.8.18/jquery-ui.min.js"></script>
        <script type="text/javascript" src="jquery.dynotable.js"></script>
        <script type="text/javascript">
            $(document).ready(function() {                
                /*
                 * Table of beers, created with some custom config options and callbacks.
                 */
                $('#beers').dynoTable({
                    removeClass: '.remove-beer',            //Custom remover class name in beers table 
                    cloneClass: '.clone-beer',              //Custom cloner class name in beers table 
                    addRowTemplateId: '#add-beer-template', //Custom id for beer row template 
                    addRowButtonId: '#add-beer',            //Click this to add a beer!
                    lastRowRemovable: false,                //Don't let the table be empty. Never run out of beer!
                    orderable: true,                        //beers can be rearranged
                    dragHandleClass: ".drag-beer",          //class for the click and draggable drag handle
                    onRowRemove: function(){
                        updateBeerCount();
                        $('#msg').html("<span style='color:crimson'>Take one down, pass it around!</span>");
                    },
                    onRowClone: function(){
                        updateBeerCount();
                        $('#msg').html("<span style='color:orange'>You cloned a beer, nice job.</span>");
                    },
                    onRowAdd: function(){
                        var numBeers = updateBeerCount();
                        $('#msg').html("<span style='color:forestgreen'>" + numBeers +  " bottles of beer on the wall, woohoo!</span>");
                    },
                    onRowReorder: function(){
                        updateBeerCount();
                        $('#msg').html("<span style='color:blue'>Beers got rearranged and renumbered</span>");
                    }
                }); 
                
                updateBeerCount(); //initial bottles of beer
            });
            
            /**
             * Updates the current beer count 
             */
            function updateBeerCount() {
                var count = 0;
                $('.beer').each(function(){ 
                    count++;
                    var msg = (count == 1) ? "1 bottle" : count + " bottles";
                    $(this).html(msg + " of beer on the wall!");
                });
                return count;
            }
        </script>
    </head>
    <body>
        <table id="beers">
            <tr>
                <td>
                    <img class="drag-beer" src="drag.png" alt="click and drag to rearrange" />
                </td>
                <td class="beer">

                </td>
                <td>
                    <img class="clone-beer" src="clone.png" alt="Clone Row" />                        
                </td>
                <td>
                    <img class="remove-beer" src="remove.png" alt="Remove Row" />
                </td>
            </tr>            
            <tr>
                <td>
                    <img class="drag-beer" src="drag.png" alt="click and drag to rearrange" />
                </td>
                <td class="beer">

                </td>
                <td>
                    <img class="clone-beer" src="clone.png" alt="Clone Row" />                        
                </td>
                <td>
                    <img class="remove-beer" src="remove.png" alt="Remove Row" />
                </td>
            </tr>  
            <tr id="add-beer-template">
                <td>
                    <img class="drag-beer" src="drag.png" alt="click and drag to rearrange" />
                </td>
                <td class="beer">
                    <!-- Beer text will go here  -->
                </td>
                <td>
                    <img class="clone-beer" src="clone.png" alt="Clone Row" />                        
                </td>
                <td>
                    <img class="remove-beer" src="remove.png" alt="Remove Row" />
                </td>
            </tr>
        </table>
        <div id="msg">
            &nbsp;
        </div>
        <button id="add-beer">Add a Beer!</button>
    </body>
</html>
<!DOCTYPE html>
<html>
    <head>
        <title></title>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
        <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jqueryui/1.8.18/jquery-ui.min.js"></script>
        <script type="text/javascript" src="jquery.dynotable.js"></script>
        <script type="text/javascript">
            $(document).ready(function() {                
                /*
                 * Table of beers, created with some custom config options and callbacks.
                 */
                $('#beers').dynoTable({
                    removeClass: '.remove-beer',            //Custom remover class name in beers table 
                    cloneClass: '.clone-beer',              //Custom cloner class name in beers table 
                    addRowTemplateId: '#add-beer-template', //Custom id for beer row template 
                    addRowButtonId: '#add-beer',            //Click this to add a beer!
                    lastRowRemovable: false,                //Don't let the table be empty. Never run out of beer!
                    orderable: true,                        //beers can be rearranged
                    dragHandleClass: ".drag-beer",          //class for the click and draggable drag handle
                    onRowRemove: function(){
                        updateBeerCount();
                        $('#msg').html("<span style='color:crimson'>Take one down, pass it around!</span>");
                    },
                    onRowClone: function(){
                        updateBeerCount();
                        $('#msg').html("<span style='color:orange'>You cloned a beer, nice job.</span>");
                    },
                    onRowAdd: function(){
                        var numBeers = updateBeerCount();
                        $('#msg').html("<span style='color:forestgreen'>" + numBeers +  " bottles of beer on the wall, woohoo!</span>");
                    },
                    onRowReorder: function(){
                        updateBeerCount();
                        $('#msg').html("<span style='color:blue'>Beers got rearranged and renumbered</span>");
                    }
                }); 
                
                updateBeerCount(); //initial bottles of beer
            });
            
            /**
             * Updates the current beer count 
             */
            function updateBeerCount() {
                var count = 0;
                $('.beer').each(function(){ 
                    count++;
                    var msg = (count == 1) ? "1 bottle" : count + " bottles";
                    $(this).html(msg + " of beer on the wall!");
                });
                return count;
            }
        </script>
    </head>
    <body>
        <table id="beers">
            <tr>
                <td>
                    <img class="drag-beer" src="drag.png" alt="click and drag to rearrange" />
                </td>
                <td class="beer">
 
                </td>
                <td>
                    <img class="clone-beer" src="clone.png" alt="Clone Row" />                        
                </td>
                <td>
                    <img class="remove-beer" src="remove.png" alt="Remove Row" />
                </td>
            </tr>            
            <tr>
                <td>
                    <img class="drag-beer" src="drag.png" alt="click and drag to rearrange" />
                </td>
                <td class="beer">
 
                </td>
                <td>
                    <img class="clone-beer" src="clone.png" alt="Clone Row" />                        
                </td>
                <td>
                    <img class="remove-beer" src="remove.png" alt="Remove Row" />
                </td>
            </tr>  
            <tr id="add-beer-template">
                <td>
                    <img class="drag-beer" src="drag.png" alt="click and drag to rearrange" />
                </td>
                <td class="beer">
                    <!-- Beer text will go here  -->
                </td>
                <td>
                    <img class="clone-beer" src="clone.png" alt="Clone Row" />                        
                </td>
                <td>
                    <img class="remove-beer" src="remove.png" alt="Remove Row" />
                </td>
            </tr>
        </table>
        <div id="msg">
            &nbsp;
        </div>
        <button id="add-beer">Add a Beer!</button>
    </body>
</html>
Example of Custom Configuration of dynoTable

Source Code
Below is the full source code of the dynoTable plugin for those who might find it useful. I am placing this code in the public domain and you may do with it as you wish. You can also download the javascript file here.

/* 
 *  jquery.dynotable.js
 *  Created on Aug 1, 2011 3:36:39 PM by bob
 */
(function($){
    $.fn.extend({
        dynoTable: function(options) {
            
            var defaults = {
                removeClass: '.row-remover',
                cloneClass: '.row-cloner',
                addRowTemplateId: '#add-template',
                addRowButtonId: '#add-row',
                lastRowRemovable: true,
                orderable: true,
                dragHandleClass: ".drag-handle",
                insertFadeSpeed: "slow",
                removeFadeSpeed: "fast",
                hideTableOnEmpty: true,
                onRowRemove: function(){},
                onRowClone: function(){},
                onRowAdd: function(){},
                onTableEmpty: function(){},
                onRowReorder: function(){}
            };     
            
            options = $.extend(defaults, options);
                                                                        
            var cloneRow = function(btn) {
                var clonedRow = $(btn).closest('tr').clone();  
                var tbod = $(btn).closest('tbody');
                insertRow(clonedRow, tbod); 
                options.onRowClone();
            }
                        
            var insertRow = function(clonedRow, tbod) {                
                var numRows = $(tbod).children("tr").length;
                if(options.hideTableOnEmpty && numRows == 0) {
                    $(tbod).parents("table").first().show();
                }
                
                $(clonedRow).find('*').andSelf().filter('[id]').each( function() {
                    //change to something else so we don't have ids with the same name
                    this.id += '__c';
                });

                //finally append new row to end of table                           
                $(tbod).append( clonedRow );
                bindActions(clonedRow);
                $(tbod).children("tr:last").hide().fadeIn(options.insertFadeSpeed);
            }
                        
            var removeRow = function(btn) {
                var tbod = $(btn).parents("tbody:first");
                var numRows = $(tbod).children("tr").length;
        
                if(numRows > 1 || options.lastRowRemovable === true) {
                    var trToRemove = $(btn).parents("tr:first");
                    $(trToRemove).fadeOut(options.removeFadeSpeed, function() {
                        $(trToRemove).remove();
                        options.onRowRemove();
                        if(numRows == 1) {                            
                            if(options.hideTableOnEmpty) {
                                $(tbod).parents('table').first().hide();
                            }
                            options.onTableEmpty();
                        }
                    });
                }                            
            }
                        
            var bindClick = function(elem, fn) {
                $(elem).click(fn);                
            }                  
                        
            var bindCloneLink = function(lnk) {
                bindClick(lnk, function(){                                
                    var btn = $(this);
                    cloneRow(btn); 
                    return false;
                });
            }
                        
            var bindRemoveLink = function(lnk) {
                bindClick(lnk, function(){ 
                    var btn = $(this);
                    removeRow(btn);
                    return false;
                });
            }
                        
            var bindActions = function(obj) {              
                obj.find(options.removeClass).each(function() {
                    bindRemoveLink($(this));
                });

                obj.find(options.cloneClass).each(function() {
                    bindCloneLink($(this));
                });
            }
         
            return this.each(function() {                             
                //Sanity check to make sure we are dealing with a single case
                if(this.nodeName.toLowerCase() == 'table') {                                
                    var table = $(this);
                    var tbody = $(table).children("tbody").first();
                                
                    if(options.orderable && jQuery().sortable) {                        
                        $(tbody).sortable({
                            handle : options.dragHandleClass,
                            helper:  function(e, ui) {
                                ui.children().each(function() {
                                    $(this).width($(this).width());
                                });
                                return ui;
                            },
                            items: "tr",
                            update : function (event, ui) {
                                options.onRowReorder();
                            }
                        });
                    }                                 
                                
                    $(table).find(options.addRowTemplateId).each(function(){
                        $(this).removeAttr("id");
                        var tmpl = $(this);
                        tmpl.remove();                        
                        bindClick($(options.addRowButtonId), function(){ 
                            var newTr = tmpl.clone();
                            insertRow(newTr, tbody);
                            options.onRowAdd();
                            return false;
                        });
                    });                                
                    bindActions(table);
                    
                    var numRows = $(tbody).children("tr").length;
                    if(options.hideTableOnEmpty && numRows == 0) {
                        $(table).hide();
                    }
                }                 
            });
        }
    });
})(jQuery);

/* 
 *  jquery.dynotable.js
 *  Created on Aug 1, 2011 3:36:39 PM by bob
 */
(function($){
    $.fn.extend({
        dynoTable: function(options) {
            
            var defaults = {
                removeClass: '.row-remover',
                cloneClass: '.row-cloner',
                addRowTemplateId: '#add-template',
                addRowButtonId: '#add-row',
                lastRowRemovable: true,
                orderable: true,
                dragHandleClass: ".drag-handle",
                insertFadeSpeed: "slow",
                removeFadeSpeed: "fast",
                hideTableOnEmpty: true,
                onRowRemove: function(){},
                onRowClone: function(){},
                onRowAdd: function(){},
                onTableEmpty: function(){},
                onRowReorder: function(){}
            };     
            
            options = $.extend(defaults, options);
                                                                        
            var cloneRow = function(btn) {
                var clonedRow = $(btn).closest('tr').clone();  
                var tbod = $(btn).closest('tbody');
                insertRow(clonedRow, tbod); 
                options.onRowClone();
            }
                        
            var insertRow = function(clonedRow, tbod) {                
                var numRows = $(tbod).children("tr").length;
                if(options.hideTableOnEmpty && numRows == 0) {
                    $(tbod).parents("table").first().show();
                }
                
                $(clonedRow).find('*').andSelf().filter('[id]').each( function() {
                    //change to something else so we don't have ids with the same name
                    this.id += '__c';
                });
 
                //finally append new row to end of table                           
                $(tbod).append( clonedRow );
                bindActions(clonedRow);
                $(tbod).children("tr:last").hide().fadeIn(options.insertFadeSpeed);
            }
                        
            var removeRow = function(btn) {
                var tbod = $(btn).parents("tbody:first");
                var numRows = $(tbod).children("tr").length;
        
                if(numRows > 1 || options.lastRowRemovable === true) {
                    var trToRemove = $(btn).parents("tr:first");
                    $(trToRemove).fadeOut(options.removeFadeSpeed, function() {
                        $(trToRemove).remove();
                        options.onRowRemove();
                        if(numRows == 1) {                            
                            if(options.hideTableOnEmpty) {
                                $(tbod).parents('table').first().hide();
                            }
                            options.onTableEmpty();
                        }
                    });
                }                            
            }
                        
            var bindClick = function(elem, fn) {
                $(elem).click(fn);                
            }                  
                        
            var bindCloneLink = function(lnk) {
                bindClick(lnk, function(){                                
                    var btn = $(this);
                    cloneRow(btn); 
                    return false;
                });
            }
                        
            var bindRemoveLink = function(lnk) {
                bindClick(lnk, function(){ 
                    var btn = $(this);
                    removeRow(btn);
                    return false;
                });
            }
                        
            var bindActions = function(obj) {              
                obj.find(options.removeClass).each(function() {
                    bindRemoveLink($(this));
                });
 
                obj.find(options.cloneClass).each(function() {
                    bindCloneLink($(this));
                });
            }
         
            return this.each(function() {                             
                //Sanity check to make sure we are dealing with a single case
                if(this.nodeName.toLowerCase() == 'table') {                                
                    var table = $(this);
                    var tbody = $(table).children("tbody").first();
                                
                    if(options.orderable && jQuery().sortable) {                        
                        $(tbody).sortable({
                            handle : options.dragHandleClass,
                            helper:  function(e, ui) {
                                ui.children().each(function() {
                                    $(this).width($(this).width());
                                });
                                return ui;
                            },
                            items: "tr",
                            update : function (event, ui) {
                                options.onRowReorder();
                            }
                        });
                    }                                 
                                
                    $(table).find(options.addRowTemplateId).each(function(){
                        $(this).removeAttr("id");
                        var tmpl = $(this);
                        tmpl.remove();                        
                        bindClick($(options.addRowButtonId), function(){ 
                            var newTr = tmpl.clone();
                            insertRow(newTr, tbody);
                            options.onRowAdd();
                            return false;
                        });
                    });                                
                    bindActions(table);
                    
                    var numRows = $(tbody).children("tr").length;
                    if(options.hideTableOnEmpty && numRows == 0) {
                        $(table).hide();
                    }
                }                 
            });
        }
    });
})(jQuery);
