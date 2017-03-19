<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
   
    
    <style>
        .password{width:auto;}
        li>span{width: 500px;border: 1px;margin-left: 20px;}
        li>span[contenteditable]{margin-left: 5px; border: 2px;width: 100px;}
        li>span[contenteditable]:hover{background-color:aqua;}
        li>span[contenteditable]:focus{background-color:chartreuse;border: 2px;width: 100px;}
    </style>
</head>
<body>
    <form >
       <label for="password">password</label>
    <input class="password" type="text" autofocus title="请设置密码，第一个为特殊字符且至少六位至少一个数字至少一个字母" 
    pattern="^[\W](?=.{5,})(?![^A-Za-z]+$)(?![^0-9]+$).*$">
    </form>
    
    <div>
        <p>请输入个人信息<p>
        <ul data-url="/users/1">
            <li>姓名<span id="name" contenteditable="true">name</span></li>
            <li>性别<span id="sex" contenteditable="true">sex</span></li>
            <li>籍贯<span id="native place" contenteditable="true">native place</span></li>
            <li>住址<span id="address" contenteditable="true">address</span></li>
        </ul>
        
    </div>
     <script src="js/jquery-3.1.1.min.js" type="text/javascript"></script>
    <script>
    $("#edit_profile_link").hide();
        var status=$("#status");
        $("span[concenteditable]").blur(function(){
            var field=$(this).attr("id");
            var value=$(this).text();
            var resourceURL=$(this).closest("ul").attr("data-url");
            $.ajax({
                
                url:resourceURL,
                dataType:"json",
                method:"PUT",
                data:field+"="+value,
                success:Function(data){
                status.html("THE record was saved.");
            },
                   Error:Function(data){
                status.html("the record failed to save.");
                
            });
            });
        }
    </script>
</body>
</html>
