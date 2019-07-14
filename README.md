Creating a Ajax's Call in word-press without a form

> this example will take your first and last name and change it to
> uppercase

**Front_End_Page.php**

    <div>
      <input id="fname" name="fname" />
        <input id="lastname" name="lastname" />
        <button id="btnSend">Send</button>
    </div>
    <div id="showResult">
    </div>

**Jquery.js**

    $("#btnSend").on('click', function (e) {
    fname = $('#fname').val();
    lastname = $('#lastname').val();
    	$.ajax({
    			url:  "/wp-admin/admin-ajax.php",
    			type: 'post',
    			data:{
    				action: 'submit_this_form',
    				fname :fname,
    				lastname:lastname
    			},
    	success: function(data){
    	   $('#showResult').html(data);
    	}
    	});
    });

**functions.php** *:this file is located in themes(wordpress) *

    function submit_this_form(){  
		  $fname = $_POST['fname'];
	   	  $lastname = $_POST['lastname'];
	   	   echo strtoupper($fname);
	   	   echo strtoupper($lastname);
      die();  
    }  
    add_action('wp_ajax_submit_this_form', 'submit_this_form');  
    add_action('wp_ajax_nopriv_submit_this_form', 'submit_this_form');

