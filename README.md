# acejs-editor-nightwing-toolbarHTML-Update
ACE JS Editor nightwing example on toolbar.html updated 
should be embeded inside the HTML tags with Body tag. Edit to suite your use.
 ![ACE Editor](git://github.com/ajaxorg/ace.git) with View Window pluse Send button, div Screen capture using HTML2Canvas and many more

    <style>
    
    .ace_editor, .toolbar {
        border: 1px solid lightgray;
        margin-left: 30px;     
        width: 50%;
    } 
    .ace_editor {
        height: auto;
    }
    
    #editor{
        margin-bottom: 30px;
        /*"margin:2px; max-width:60px;padding:5px;max-height:25px;"*/
      /*  style: "margin:2px; max-width:60px;padding:5px;max-height:25px;", */
    }
    .toolbar{
        margin-top: 40px;
    }
    #previewContainer{
        border: 10px solid #eee;
        width: 30%;
        padding: 20px;
        margin-right: 10px;
        margin-top: 10px;
        height: 450px;
        overflow: scroll;
        float: right;

    }

    
    </style>

    <select id="theme_selector" class="col-xs-offset-1" style="max-width:160px">
            
            <option value="" selected>Select editor's theme</option>
            <option value="chrome">Chrome</option>
            <option value="crimson_editor">Crimson</option>
            <option value="ambiance">Ambiance</option>            
            <option value="github">Github</option>
            <option value="textmate">Textmate</option>
            <option value="dreamweaver">Dreamweaver</option>           
            <option value="eclipse">Eclipse</option>            
            <option value="twilight">Twilight</option>         
            <option value="vibrant_ink">Vibrant ink</option>
            <option value="tomorrow_night_eighties">Tomorrow night 80s</option>
        
        </select><br>
        
        <label class="col-xs-offset-1" for="amount">Design Price:</label>
        
        <input class="col-xs-offset-1" style="max-width:160px" type="text" id="amt" placeholder="Amount"/><br>
        
        <label class="col-xs-offset-1" for="version">Version Design:</label>
        
        <input class="col-xs-offset-1" style="max-width:160px" type="text" id="version" placeholder="Version"/><br>
        
    <div class="radio-option">
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Choose Design:<br>
        <input type="radio" id="c_v" class="radioType" name="type" value="radio1" />
        <label for="c_v">CV</label>
        <input type="radio" id="c_l" class="radioType" name="type" value="radio2" />
        <label for="c_l">Cover Letter</label>
        <input type="radio" id="p_l" class="radioType" name="type" value="radio3" />
        <label for="p_l">Proposal Letter</label>       
    </div>
        <p id="msg" style="margin-left: 30px; color: red"></p>
        <div id="editor">
        </div>
        <div id="previewContainer">
            <p class="pull-left" style="position: absolute; z-index:1; background: rgba(0,0,0,0.7); padding:5px; border-radius:2px; border: 1px solid rgba(0,0,0,0.5); color:#fff">OUTPUT</p>
            <button id="saveBtn" style="position: absolute; right:25px; z-index:1;max-width: 60px; max-height: 25px; margin-right:30px; padding:5px;">Save</button>
            <p id="msgOut" align="center" style="position: absolute; z-index:1;color:red;padding:5px;"></p>
            <div id="preview1" style="padding:20px;eight:842px; width:595px;" ></div> <!--"height:842px; width:595px;"-->
        </div>
        
        <input id="coder_id" type="hidden" value="<?php if(isset($this->session->userdata['is_logged_in'])){ $coderID = $this->session->userdata['is_logged_in']['reg_id']; echo $coderID; } ?>"/>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.4.1/ace.js" ></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.4.1/ext-modelist.js" ></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.4.1/ext-error_marker.js" ></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.4.1/ext-language_tools.js" ></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.4.1/ext-options.js" ></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.4.1/mode-javascript.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.4.1/worker-javascript.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.4.1/theme-chrome.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.4.1/theme-crimson_editor.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.4.1/theme-ambiance.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.4.1/theme-github.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.4.1/theme-textmate.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.4.1/theme-dreamweaver.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.4.1/theme-eclipse.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.4.1/theme-twilight.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.4.1/theme-vibrant_ink.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ace/1.4.1/mode-php.js"></script>
    <script src="<?php echo base_url(); ?>assets/js/html2canvas.min.js"></script>

    <script>
        $(document).ready(function(){
        //Mvhd addition for displaying output on clicking save in the editor
         var editorValue = editor.getValue();
         document.getElementById('preview1').innerHTML= ""+editorValue; 
    });
     
    var buildDom = require("ace/lib/dom").buildDom;
    var editor = ace.edit('editor');
    editor.setOptions({
        enableBasicAutocompletion: true, // the editor completes the statement when you hit Ctrl + Space
        enableLiveAutocompletion: true,
        theme: "ace/theme/tomorrow_night_eighties",
        mode: "ace/mode/markdown",
        maxLines: 30,
        minLines: 30,
        autoScrollEditorIntoView: true,
        tabSize: 4,
        useSoftTabs: true
    });
    
    $('#theme_selector').on('change',function(){
             var theme = $('#theme_selector').val(); 
    
    editor.setTheme("ace/theme/"+theme); // Mvhd addition to choose editor's theme chrome,crimson_editor,tomorrow_night_eighties,ambiance,github,textmate
    });
    var refs = {};
    function updateToolbar() {
        refs.saveButton.disabled = editor.session.getUndoManager().isClean();
        refs.undoButton.disabled = !editor.session.getUndoManager().hasUndo();
        refs.redoButton.disabled = !editor.session.getUndoManager().hasRedo();
        refs.sendButton.disabled = editor.session.getUndoManager().isClean(); //Mvhd addition
    }
    editor.on("input", updateToolbar);
    editor.session.setValue(localStorage.savedValue || "Welcome to ace Toolbar demo!")
    function save() {
        localStorage.savedValue = editor.getValue(); 
        editor.session.getUndoManager().markClean();
        var editorValue = editor.getValue();
        document.getElementById('preview1').innerHTML= ""+editorValue; 
        updateToolbar();
    }
    editor.commands.addCommand({
        name: "save",
        exec: save,
        bindKey: { win: "ctrl-s", mac: "cmd-s" }
    });
    
    //1. Mvhd addition starts

    function post() {
     
        var coderId = $('#coder_id').val();
        var version = $('#version').val();
        var amount = $('#amt').val();
        var editorValue = editor.getValue();
        
        setTimeout(function(){
                $('#msg').hide('slow');
            },5000);
       
        if(version.length===0){
            $('#msg').html('provide design version');
            $('#msg').css({'background':'#fff','border':'1px solid #000','width':'170px','padding':'3px'});
            return false;
        }
        if(amount.length===0){
            $('#msg').html('provide price or amount');
            $('#msg').css({'background':'#fff','border':'1px solid #000','width':'170px','padding':'3px'});
            return false;    
        }
        if(editorValue.length===0){
            $('#msg').html('you cant submit empty script');
            $('#msg').css({'background':'#fff','border':'1px solid #000','width':'170px','padding':'3px'});
            return false;
        }
        
        if($("input:radio[name='type'].radioType").is(":checked")){
            var output = $("input:radio[name='type'].radioType:checked").val();
        }else{
            $('#msg').html('Select an option to proceed');
            $('#msg').css({'background':'#fff','border':'1px solid #000','width':'170px','padding':'3px'});
            return false;
        }
        html2canvas($('#preview1')[0]).then(function(canvas) {
            var dataUrl = canvas.toDataURL();
            var newDataURL = dataUrl.replace(/^data:image\/png/, "data:application/octet-stream");
            $("#saveBtn").attr("download", "your_pic_name.png").attr("href", newDataURL);
      
        $.ajax({
            'type': 'post',
            'url': 'login/insert_coderto_db',
            data: {
                'radio_value':output+'-'+version,
                'editor_value':editorValue,
                'amount':amount,
                'reg_id':coderId,
                'img':newDataURL
            },
            success: function(data){

                var dt = JSON.parse(data);
                if(dt.message===1){
                    $('#msg').html('Inserted to DB successfully.');
                    $('#msg').css({'background':'#fff','border':'1px solid #000','width':'170px','padding':'3px'});
                    
                }else if(dt.message===0){
                    $('#msg').html('Oops! Unable to insert to DB.');
                    $('#msg').css({'background':'#fff','border':'1px solid #000','width':'170px','padding':'3px'});
                    return false;
                }
                refs.sendButton.disabled = editor.session.getUndoManager().isClean();
            },
            error: function(data){
                console.log(data);
            }
        });
        
        });
        
        //updateToolbar();
    }
    editor.commands.addCommand({
        name: "send",
        exec: post,
       bindKey: { win: "ctrl-s", mac: "cmd-s" }
    });
    //1. Mvhd addition ends
    
    buildDom(["div", { class: "toolbar" },
              //2. CVB addition start
        ["button", {
            ref: "sendButton",
            style: "margin:2px; max-width:60px;padding:5px;max-height:25px; background:green",
            onclick: post
        }, "send"],
              //2.Mvhd addition end
        ["button", {
            ref: "saveButton",
            style: "margin:2px; max-width:60px;padding:5px;max-height:25px;",
            onclick: save
        }, "save"],
        ["button", {
            ref: "undoButton",
            style: "margin:2px; max-width:60px;padding:5px;max-height:25px;",
            onclick: function() {
                editor.undo();
            }
        }, "undo"],
        ["button", {
            ref: "redoButton",
            style: "margin:2px; max-width:60px;padding:5px;max-height:25px;",
            onclick: function() {
                editor.redo();
            }
        }, "redo"],
        ["button", {
            style: "font-weight: bold;margin:2px; max-width:60px;padding:5px;max-height:25px;",
            onclick: function() {
                editor.insertSnippet("**${1:$SELECTION}**");
                editor.renderer.scrollCursorIntoView()
            }
        }, "bold"],
        ["button", {
            style: "font-style: italic;margin:2px; max-width:60px;padding:5px;max-height:25px;",
            onclick: function() {
                editor.insertSnippet("*${1:$SELECTION}*");
                editor.renderer.scrollCursorIntoView()
            }
        }, "Italic"],
    ], document.body, refs);
    document.body.appendChild(editor.container)
    
    window.editor = editor;
