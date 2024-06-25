# wuhuchengdongyiyuan
<!DOCTYPE HTML>

<html xmlns="http://www.w3.org/1999/xhtml" xmlns:sec="http://www.thymeleaf.org/thymeleaf-extras-springsecurity3">
<head>
	<meta charset="UTF-8" />
	<meta http-equiv="X-UA-Compatible" />
	<title>云影通 - 登录</title>
	<link type="text/css" rel="stylesheet" href="/phantomcz/webapp/css/base.css" />
	<link type="text/css" rel="stylesheet" href="/phantomcz/webapp/css/login.css" />
	<link type="text/css" rel="stylesheet" href="/phantomcz/webapp/css/page.css" />
	
	<script type="text/javascript" src="/phantomcz/webapp/js/plugin/jquery-3.6.0.min.js"></script>
	<script type="text/javascript" src="/phantomcz/webapp/js/plugin/jquery.cookie.js"></script>
	<script type="text/javascript" src="/phantomcz/webapp/js/common.js"></script>
	<script type="text/javascript" src="/phantomcz/webapp/js/login.js"></script>
	<script type="text/javascript" src="/phantomcz/webapp/js/registered.js"></script>
	<script type="text/javascript" src="/phantomcz/webapp/js/plugin/My97DatePicker/WdatePicker.js"></script>
	<script type="text/javascript" src="/phantomcz/webapp/js/gdca-pki/gdca-pki-lib-s.js"></script>
	<script type="text/javascript" src="/phantomcz/webapp/js/gdca-pki/wt_base64.js"></script>
	<script type="text/javascript" src="/phantomcz/webapp/js/gdca-pki/gdca-pki-errcode.js"></script>
	<script type="text/javascript" src="/phantomcz/webapp/js/gdca-pki/js/jquery.jsonp.js"></script>
	<script type="text/javascript" src="/phantomcz/webapp/js/gdca-pki/js/json2.js"></script>
	<script type="text/javascript" src="/phantomcz/webapp/js/plugin/encryption/encryption.js"></script>
</head>
<body>

<div class="g-wrap s-bgImage1 f-pr">
	<a style="color: #ccc;" href="login?lang=zh">中文</a>
    <a style="color: #ccc;" href="login?lang=en">English</a>
    <div class="g-bd s-bgBd f-pa">
        <div class="u-nav s-fc13 f-fs16" id="loginCE">用户登录</div>
        <div class="g-left f-fl">
            <dl>
               <dt class="f-fs24 s-fc15">云影通</dt>
               <dd class="f-fs14 s-fc14">云影通是一个由医生组成的联盟或组织机构；通过云PACS平台，医生可以不受终端、场景、时间限制，随时随地查看影像，编辑、审核报告</dd>
            </dl>
            <!-- <a class="f-db s-fc16 f-fs16" id="registered" th:text="#{login.registered}">注册</a> -->
        </div>
        <div class="oneLine  f-fl"></div>
        
        <div id="userlogin" class="g-right f-fl" style="display: block;">
            <form class="f-fs16" id="loginForm" action="/phantomcz/loginprocessing" method="post">
               <p id="message" class="f-fs14  f-dn"><span class="currentSpan f-fs14">X</span><span class="LoginMessageTips" style="color:#E40E0E;">登录名或密码错误</span></p>
               <!-- <p id="message" class="f-fs14 s-fc20 f-dn" style="color:#E40E0E;">登录名或密码错误</p> -->
               <div>
                   <span class="s-fc18 f-fl">帐号</span>
                   <input class="f-fs16 s-fc19 f-fl" type="text" id="username" />
                   <input type="hidden" id="usernameHidden" name="username" />
               </div>
               <div>
                   <span class="s-fc18 f-fl">密码</span>
                   <input class="f-fs16 s-fc19 f-fl" type="password" id="password" name="password" />
               </div>
               
               
               <div class="button">
                   <input class="f-fs16 s-fc0" id="submitBtn" type="submit" value="登录" style="cursor: pointer;" />

               </div>
               <div style="background-color:#fff" class="button">
               	   <input class="f-fs16 s-fc0" id="exchangelogca" type="button" value="切换CA登陆" style="cursor: pointer;color:#ccc" />
               </div>
            </form>
        </div>
        <div id="calogin" class="g-right f-fl" style="display: none;">
            <form class="f-fs16" id="caloginForm" action="/phantomcz/task" method="post">
               <p id="messageca" class="f-fs14 f-dn"><span class="currentSpan f-fs14">X</span><span class="LoginMessageTips" style="color:#E40E0E;">登录名或密码错误</span></p>
               <!-- <p id="message" class="f-fs14 s-fc20 f-dn" style="color:#E40E0E;">登录名或密码错误</p> -->
               <div>
                   <span class="s-fc18 f-fl">用户：</span>
                   <select id="caUsername" class="f-fs16 s-fc19 f-fl" style="width: 80%;height: 100%;background: 0;border: 0;box-sizing: border-box;padding-left: .8rem;color: #42596f;display: inline-block;float: right;">
                   </select>
                   <input type="hidden" name="CertID" value="" />
               </div>
               <div>
                   <span class="s-fc18 f-fl">PIN：</span>
                   <input class="f-fs16 s-fc19 f-fl" type="password" id="userPin" name="userPin" style="display: inline-block;float: right;" />
               </div>
               <div class="u-remeber">
                   <!-- <input type="checkbox" id="autoLogin"/> -->
                   <label for="autoLogin" class="s-fc17 f-fs14"></label></div>
               <div class="button">
                   <input class="f-fs16 s-fc0" id="submitBtnca" type="submit" value="登录" style="cursor: pointer;" />
               </div>
               <div class="button" style="background-color:#fff">
                   <input class="f-fs16 s-fc0" id="exchangelog" type="button" value="切换账号登陆" style="cursor: pointer;color:#ccc" />
               </div>
            </form>
        </div>
    </div>
    <div class="model" id="registered-model">
    <!-- 
    	<div class="registered-div">
    		<div class="registered-top">
    			<span id="registered-title" th:text="#{login.login}+'(*'+#{login.required}+')'">注册(*为必填项)</span>
	            <span>X</span>
    		</div>
    		<form action="registered" id="registeredSubmit" method="post" enctype="multipart/form-data">
    		<div class="registered-content">
    			<ul>
    				<li>
    					<span th:text="#{login.username}+' *'">帐号*</span>
    					<input type="text" name="username" value="" id="addusername"/>
    				</li>
    				<li>
    					<span th:text="#{login.name}+' *'">姓名*</span>
    					<input type="text" name="name" value="" id="addname"/>
    				</li>
    				<li>
    					<span th:text="#{login.password}+' *'">密码*</span>
    					<input type="password" name="password" value="" id="addpassword" />
    				</li>
    				<li>
    					<span th:text="#{login.Cpassword}+' *'">确认密码*</span>
    					<input type="password" value="" id="addpasswords" />
    				</li>
    				<li>
    					<span th:text="#{login.gender}">性别</span>
    					<select id="addgender" name="gender">
    						<option value="1" th:text="#{task.male}">男</option>
    						<option value="2" th:text="#{task.female}">女</option>
    						<option value="3" th:text="#{login.Other}">其他</option>
    					</select>
    				</li>
    				<li>
    					<span th:text="#{login.dateOfBirth}">出生日期</span>
    					<input type="text" id="addbirthday" name="birthday" onfocus="WdatePicker({skin:'whyGreen',dateFmt:'yyyy-MM-dd'})"/>
    				</li>
    				<li>
    					<span th:text="#{login.phoneNO}">电话号码</span>
    					<input type="text" id="addtelNo" name="telNo"/>
    				</li>
    				<li>
    					<span th:text="#{login.homeAddress}">家庭住址</span>
    					<input type="text" id="address" name="address" />
    				</li>
    				<li>
    					<span th:text="#{login.e-mail}">邮箱</span>
    					<input type="text" id="addeMail" name="eMail" />
    				</li>
    				<li>
    					<span th:text="#{login.hospital}">医院</span>
    					<input type="text" id="hosptial" name="hosptial" />
    				</li>
    				<li>
    					<span th:text="#{login.department}">科室</span>
    					<input type="text" id="deptName" name="deptName"/>
    				</li>
    				<li>
    					<span th:text="#{login.level}">级别</span>
    					<select id="level" name="level">
    						<option th:text="#{login.intern}" value="5">实习生</option>
    						<option th:text="#{login.primary}" value="11">初级</option>
    						<option th:text="#{login.intermediate}" value="21">中级</option>
    						<option th:text="#{login.DSenior}" value="23">副高</option>
    						<option th:text="#{login.FEDoctor}" value="25">进修医生</option>
    						<option th:text="#{login.professor}" value="30">正教授</option>
    						<option th:text="#{login.director}" value="32">主任</option>
    					</select>
    				</li>
    				<li>
    					<span th:text="#{login.addsignImage}">电子签名</span>
    					<input type="file" id="addsignImage" name="addImage" />
    				</li>
    				<li>
    					<span th:text="#{login.addportImage}">执照证件</span>
    					<input type="file" id="addportImage" name="addImage" />
    				</li>
    				<li>
    					<span th:text="#{login.addcardImage}">身份证件</span>
    					<input type="file" id="addcardImage" name="addImage"/>
    				</li>
    				<li>
    					<span>申请工作室</span>
    					<select id="addstudioID" name="addstudioID">
    					</select>
    				</li>
    				<li>
    					<span th:text="#{login.comment}">备注</span>
    					<textarea  id="comment" name="comment"></textarea>
    				</li>
    				<li>
    					<input type="button" class="registered-input" id="registered-input" th:value="#{login.registered}" value="注册"/>
    				</li>
    			</ul>
    		</div>
    		</form>
    	</div>-->
    </div>
</div>
</body>
<script>
  /*<![CDATA[*/
        var phoneVF = '0';
  /*]]>*/
</script>
</html>
