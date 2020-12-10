# Assignment
JQueryUI



<!doctype html>
<html lang="en">
<head>
    <title>Q11</title>
    <script  src="jsMinified.js" > </script>
    <script src="jquery-ui.js"></script>
</head>
<script type="text/javascript">

    $(function () { 
        

        var new_dialog = function (type, row) {

            var dlg = $("#dialog-form").clone();

            var fname = dlg.find(("#first-name")),

        lname = dlg.find(("#last-name")),

        email = dlg.find(("#email")),

        password = dlg.find(("#password"));

            type = type || 'Create';

            var config = {

                autoOpen: true,

                height: 300,

                width: 350,

                modal: true,

                buttons: {

                    "Create an account": save_data,

                    "Cancel": function () {

                        dlg.dialog("close");

                    }

                },

                close: function () {

                    dlg.remove();

                }

            };

            if (type === 'Edit') {

                config.title = "Edit User";

                get_data();

                delete (config.buttons['Create an account']);

                config.buttons['Edit account'] = function () {

                    row.remove();

                    save_data(); 

                }; 

            }

            dlg.dialog(config); 

            function get_data() {

                var _email = $(row.children().get(1)).text(),

            _password = $(row.children().get(2)).text();

                email.val(_email);

                password.val(_password); 

            } 

            function save_data() {

                $("#users tbody").append("<tr>" + "<td>" + (fname.find("option:selected").text() + ' ').concat(lname.find("option:selected").text()) + "</td>" + "<td>" + email.val() + "</td>" + "<td>" + password.val() + "</td>" + "<td><a href='' class='edit'>Edit</a></td>" + "<td><span class='delete'><a href=''>Delete</a></span></td>" + "</tr>");

                dlg.dialog("close");

            }

        }; 

        $(document).on('click', 'span.delete', function () {

            $(this).closest('tr').find('td').fadeOut(1000, 

    function () {

        // alert($(this).text());

        $(this).parents('tr:first').remove();

    }); 

            return false;

        });

        $(document).on('click', 'td a.edit', function () {

            new_dialog('Edit', $(this).parents('tr'));

            return false;

        }); 

        $("#create-user").button().click(new_dialog); 

    });

</script>



Add style:

<style type="text/css">

body {

font-size: 62.5%;

}

label, input {

display: block;

}

input.text {

margin-bottom: 12px;

width: 95%;

padding: .4em;

}

fieldset {

padding: 0;

border: 0;

margin-top: 25px;

}

h1 {

font-size: 1.2em;

margin: .6em 0;

}

div#users-contain {

width: 350px;

margin: 20px 0;

}

div#users-contain table {

margin: 1em 0;

border-collapse: collapse;

width: 100%;

}

div#users-contain table td, div#users-contain table th {

border: 1px solid #eee;

padding: .6em 10px;

text-align: left;

}

.ui-dialog .ui-state-error {

padding: .3em;

}

.validateTips {

border: 1px solid transparent;

padding: 0.3em;

}

#dialog-form {

display: none;

}

</style>
<body>
    

    <div id="dialog-form" title="Create new user">

        <p class="validateTips">

            All form fields are required.</p>       

            <form>

        <fieldset>

            <label for="first_name" >

                First Name</label>

                <input type="text" id="first-name" />

            <!-- <select >

                <option value="1">Arun</option>

                <option value="2">Ganesh</option>

                <option value="3">Suresh</option>

                <option value="4">Sanganabasu</option>

            </select> -->

            
            <label for="email">

                Email</label>

            <input type="text" name="email" id="email" value="" class="text ui-widget-content ui-corner-all" />

            <label for="password">

                Password</label>

            <input type="password" name="password" id="password" value="" class="text ui-widget-content ui-corner-all" />

        </fieldset>

        </form>

    </div>

    <div id="users-contain" class="ui-widget">

        <h1>

            Existing Users:</h1>

        <table id="users" class="ui-widget ui-widget-content">

            <thead>

                <tr class="ui-widget-header ">

                    <th>Name </th>

                    <th>Email </th>

                    <th>Password</th>

                    <th> Actions</th>

                </tr>

            </thead>

            <tbody>

                <tr> <td class="custom-name"> John Doe </td>

                    <td>john.doe@example.com</td>

                    <td>johndoe1 </td>

                    <td><a class="edit" href="">Edit</a> </td>

                    <td><span class="delete"><a href="">Delete</a></span>   </td>

                </tr>

            </tbody>

        </table>

    </div>

    <button id="create-user">

        Create new user</button>   
</body>
</html>
