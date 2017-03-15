title: mailgun优秀的邮件服务器
date: 2014-07-31 14:57
tags: mailgun，邮件服务器

------
昨天晚上我一个朋友问我用什么搭建邮件服务器，我本来想问使用linux还是windows，但是我还是先问了一下他需要邮件服务器干什么？当然这个很重要，因为有时你根本不需要自己搭建一个邮件服务器。比如像他这样的，他仅仅是想用一个邮件服务器做一个测试，自己搭建一个邮件服务器未免太过于浪费，而且没有必要。所以我给他推荐了mailgun邮件服务器。
说到mailgun我又要先百科一下，好像这已经形成了我写博客的习惯，先百科介绍一下，好吧，百度没有，google也没有介绍，就连Wikipedia上也没有介绍，好吧，没有百科，并不代表他不够优秀。不信你看利用mailgun还是有一堆，
![QQ截图20140731092227.png](http://upload-images.jianshu.io/upload_images/24022-4b935b0f885aa007.png)（这个是我从DuckDuckGo上搜索截图的）
所以请不要怀疑，mailgun是开发人员最喜欢的邮件服务器，没有之一。

既然没有百科，我就自己来介绍一下mailgun吧，Mailgun 是一个简便高效的邮件发送云服务，提供丰富的API接口
![QQ截图20140731092818.png](http://upload-images.jianshu.io/upload_images/24022-1ddb263ff387295d.png)
这也是他们一直强调的一个东西，但是开发人员喜欢他，不仅是应为他具有丰富的API接口，还有就是他提供每个月3000封免费邮件发送服务，邮件到达率非常高。显然，对于开发者来说这就足够了，而且就算升级到付费版也比较便宜。当你开发程序时需要用到邮件发送服务，这时你就需要去搭建一个邮件服务器，显然这不是程序员擅长的，当然你可以去购买付费的邮件服务产品，但是我跟喜欢免费产品。

自己搭建邮件服务器也没有什么不靠谱的，windows自带就有邮件服务功能，只需要添加即可。当然你也可以使用其他产品，例如Hmailserver（我自己建了一个Hmailserver中文论坛，http://hmailserver.7keji.cn/ 你可以在这里寻求帮助，我们公司就是采用这个，一直在使用，很稳定，垃圾邮件过滤也很赞！），Apache james以及其他免费产品。如果你是选择linux的话，免费的邮件服务就更多了，而且大多都是开源的。当然你也可以选择一些商业版的，例如Google，SendCloud等付费产品。上面说到过，自己搭建是没有必要的，我们已经有了这么优秀的免费邮件服务器为什么还要自己花费时间去搭建呢，虽然难度不大，但是还是需要我们花费很多时间。而且如果你要把他发布在互联网测试的话，你还需要一个静态的IP地址，而且新建邮件服务器一般不被认可，大部分邮件直接当垃圾邮件处理了。这显然不是我们想要的，所以mailgun足够了。

好了，说了这么多废话我就来讲一下mailgun的使用吧，虽然比较简单，但是毕竟有些人（呵呵，我就不点名了）还是有需求的。
1、注册
打开mailgun官网http://www.mailgun.com/ （昨天他反应打开比较慢，所以你得有点耐心，或者跟换你的DNS试试）

![QQ截图20140731095618.png](http://upload-images.jianshu.io/upload_images/24022-fa47346acc66cd8a.png)

点击 “Try Mailgun Now”跟一般网站注册一样，填写注册信息

![QQ截图20140731095810.png](http://upload-images.jianshu.io/upload_images/24022-7f622cd8bfa7c0f0.png)
点击注册即可。
2、设置
注册完后直接登录
![QQ截图20140731095952.png](http://upload-images.jianshu.io/upload_images/24022-b9cf9ce8bca93daa.png)
登陆后查看有边信息，上面是如果你有自己的域名，你可以直接绑定域名，下面是给我们提供的免费域名，本次用于测试，直接选用免费域名即可。

![QQ截图20140731100231.png](http://upload-images.jianshu.io/upload_images/24022-0878c00d0232c6c8.png)
点击Active即跳转到设置页面。里面列出了SMTP服务器，和自动创建了一个测试用户以及密码。
![QQ截图20140731100519.png](http://upload-images.jianshu.io/upload_images/24022-12d6ecc50e9621f7.png)
你也可以再添加用户点击账户后面的“Manage SMTP credentials”即可进入到添加用户界面，这里我们仅用于测试一个就够了，因为它可以直接向你Gmail或 QQ邮箱发送邮件了，所以你不必再去添加一个接收邮件的账户了。
![QQ截图20140731100651.png](http://upload-images.jianshu.io/upload_images/24022-4bb5b7701aa5b41c.png)

3、客户端设置

windows的邮件客户端还是比较多的，比如Foxmail ，Outlook，Thurdbird等。linux也有不少。设置页很简单，我们用Foxmail来做测试，毕竟他是微信之父张小龙的产品。她也一直是我的偶像。
好了，我们利用foxmail新建一个账户，输入刚才看到的账户和密码。

![QQ截图20140731101217.png](http://upload-images.jianshu.io/upload_images/24022-60596a355c3ead80.png)
点击下一步

![QQ截图20140731101449.png](http://upload-images.jianshu.io/upload_images/24022-ccf6aaa9dc59ccdb.png)
这里我们选择网站提供给我们的SMTP服务器地址smtp.mailgun.org，Oh,sorry! Mailgun好像没有提供邮件接收服务器，所以我们这里登录不了，只能采用其他的方式。（这里我不确定，我刚才已经发送tweet给mailgun的官方 twitter了，到时看看他们怎么回复我）

好吧我们在这里写一个简单的PHP邮件发送工具
复制代码，另存为email.class.php
         <?php
        class smtp
    {
    / Public Variables /

    var $smtp_port;

    var $time_out;

    var $host_name;

    var $log_file;

    var $relay_host;

    var $debug;

    var $auth;

    var $user;

    var $pass;

    /* Private Variables */
    var $sock;

    /* Constractor */

    function smtp($relay_host = "", $smtp_port = 25,$auth = false,$user,$pass)

    {

    $this->debug = FALSE;

    $this->smtp_port = $smtp_port;

    $this->relay_host = $relay_host;

    $this->time_out = 30; //is used in fsockopen()
    #

    $this->auth = $auth;//auth

    $this->user = $user;

    $this->pass = $pass;

    #

    $this->host_name = "localhost"; //is used in HELO command
    $this->log_file = "";

    $this->sock = FALSE;

    }

    /* Main Function */

    function sendmail($to, $from, $subject = "", $body = "", $mailtype, $cc = "", $bcc = "", $additional_headers = "")

    {

    $mail_from = $this->get_address($this->strip_comment($from));

    $body = ereg_replace("(^|(\r\n))(\.)", "\1.\3", $body);

    $header = "MIME-Version:1.0\r\n";

    if($mailtype=="HTML"){

    $header .= "Content-Type:text/html\r\n";

    }

    $header .= "To: ".$to."\r\n";

    if ($cc != "") {

    $header .= "Cc: ".$cc."\r\n";

    }

    $header .= "From: $from<".$from.">\r\n";

    $header .= "Subject: ".$subject."\r\n";

    $header .= $additional_headers;

    $header .= "Date: ".date("r")."\r\n";

    $header .= "X-Mailer:By Redhat (PHP/".phpversion().")\r\n";

    list($msec, $sec) = explode(" ", microtime());

    $header .= "Message-ID: <".date("YmdHis", $sec).".".($msec*1000000).".".$mail_from.">\r\n";

    $TO = explode(",", $this->strip_comment($to));

    if ($cc != "") {

    $TO = array_merge($TO, explode(",", $this->strip_comment($cc)));

    }

    if ($bcc != "") {

    $TO = array_merge($TO, explode(",", $this->strip_comment($bcc)));

    }

    $sent = TRUE;

    foreach ($TO as $rcpt_to) {

    $rcpt_to = $this->get_address($rcpt_to);

    if (!$this->smtp_sockopen($rcpt_to)) {

    $this->log_write("Error: Cannot send email to ".$rcpt_to."\n");

    $sent = FALSE;

    continue;

    }

    if ($this->smtp_send($this->host_name, $mail_from, $rcpt_to, $header, $body)) {

    $this->log_write("E-mail has been sent to <".$rcpt_to.">\n");

    } else {

    $this->log_write("Error: Cannot send email to <".$rcpt_to.">\n");

    $sent = FALSE;

    }

    fclose($this->sock);

    $this->log_write("Disconnected from remote host\n");

    }

    return $sent;

    }

    /* Private Functions */

    function smtp_send($helo, $from, $to, $header, $body = "")

    {

    if (!$this->smtp_putcmd("HELO", $helo)) {

    return $this->smtp_error("sending HELO command");

    }

    #auth

    if($this->auth){

    if (!$this->smtp_putcmd("AUTH LOGIN", base64_encode($this->user))) {

    return $this->smtp_error("sending HELO command");

    }

    if (!$this->smtp_putcmd("", base64_encode($this->pass))) {

    return $this->smtp_error("sending HELO command");

    }

    }

    #

    if (!$this->smtp_putcmd("MAIL", "FROM:<".$from.">")) {

    return $this->smtp_error("sending MAIL FROM command");

    }

    if (!$this->smtp_putcmd("RCPT", "TO:<".$to.">")) {

    return $this->smtp_error("sending RCPT TO command");

    }

    if (!$this->smtp_putcmd("DATA")) {

    return $this->smtp_error("sending DATA command");

    }

    if (!$this->smtp_message($header, $body)) {

    return $this->smtp_error("sending message");

    }

    if (!$this->smtp_eom()) {

    return $this->smtp_error("sending <CR><LF>.<CR><LF> [EOM]");

    }

    if (!$this->smtp_putcmd("QUIT")) {

    return $this->smtp_error("sending QUIT command");

    }

    return TRUE;

    }

    function smtp_sockopen($address)

    {

    if ($this->relay_host == "") {

    return $this->smtp_sockopen_mx($address);

    } else {

    return $this->smtp_sockopen_relay();

    }

    }

    function smtp_sockopen_relay()

    {

    $this->log_write("Trying to ".$this->relay_host.":".$this->smtp_port."\n");

    $this->sock = @fsockopen($this->relay_host, $this->smtp_port, $errno, $errstr, $this->time_out);

    if (!($this->sock && $this->smtp_ok())) {

    $this->log_write("Error: Cannot connenct to relay host ".$this->relay_host."\n");

    $this->log_write("Error: ".$errstr." (".$errno.")\n");

    return FALSE;

    }

    $this->log_write("Connected to relay host ".$this->relay_host."\n");

    return TRUE;;

    }

    function smtp_sockopen_mx($address)

    {

    $domain = ereg_replace("^.+@([^@]+)$", "\1", $address);

    if (!@getmxrr($domain, $MXHOSTS)) {

    $this->log_write("Error: Cannot resolve MX \"".$domain."\"\n");

    return FALSE;

    }
    //专注与php学习 http://www.daixiaorui.com 欢迎您的访问

    foreach ($MXHOSTS as $host) {

    $this->log_write("Trying to ".$host.":".$this->smtp_port."\n");

    $this->sock = @fsockopen($host, $this->smtp_port, $errno, $errstr, $this->time_out);

    if (!($this->sock && $this->smtp_ok())) {

    $this->log_write("Warning: Cannot connect to mx host ".$host."\n");

    $this->log_write("Error: ".$errstr." (".$errno.")\n");

    continue;

    }

    $this->log_write("Connected to mx host ".$host."\n");

    return TRUE;

    }

    $this->log_write("Error: Cannot connect to any mx hosts (".implode(", ", $MXHOSTS).")\n");

    return FALSE;

    }

    function smtp_message($header, $body)

    {

    fputs($this->sock, $header."\r\n".$body);

    $this->smtp_debug("> ".str_replace("\r\n", "\n"."> ", $header."\n> ".$body."\n> "));

    return TRUE;

    }

    function smtp_eom()

    {

    fputs($this->sock, "\r\n.\r\n");

    $this->smtp_debug(". [EOM]\n");

    return $this->smtp_ok();

    }

    function smtp_ok()

    {

    $response = str_replace("\r\n", "", fgets($this->sock, 512));

    $this->smtp_debug($response."\n");

    if (!ereg("^[23]", $response)) {

    fputs($this->sock, "QUIT\r\n");

    fgets($this->sock, 512);

    $this->log_write("Error: Remote host returned \"".$response."\"\n");

    return FALSE;

    }

    return TRUE;

    }

    function smtp_putcmd($cmd, $arg = "")

    {

    if ($arg != "") {

    if($cmd=="") $cmd = $arg;

    else $cmd = $cmd." ".$arg;

    }

    fputs($this->sock, $cmd."\r\n");

    $this->smtp_debug("> ".$cmd."\n");

    return $this->smtp_ok();

    }

    function smtp_error($string)

    {

    $this->log_write("Error: Error occurred while ".$string.".\n");

    return FALSE;

    }

    function log_write($message)

    {

    $this->smtp_debug($message);

    if ($this->log_file == "") {

    return TRUE;

    }

    $message = date("M d H:i:s ").get_current_user()."[".getmypid()."]: ".$message;

    if (!@file_exists($this->log_file) || !($fp = @fopen($this->log_file, "a"))) {

    $this->smtp_debug("Warning: Cannot open log file \"".$this->log_file."\"\n");

    return FALSE;;

    }

    flock($fp, LOCK_EX);

    fputs($fp, $message);

    fclose($fp);


    return TRUE;

    }


    function strip_comment($address)

    {

    $comment = "\([^()]*\)";

    while (ereg($comment, $address)) {

    $address = ereg_replace($comment, "", $address);

    }


    return $address;

    }


    function get_address($address)

    {

    $address = ereg_replace("([ \t\r\n])+", "", $address);

    $address = ereg_replace("^.*<(.+)>.*$", "\1", $address);

    return $address;

    }

    function smtp_debug($message)

    {

    if ($this->debug) {

    echo $message;

    }

    }

    }

    ?>

复制代码另存为sendmail.php

           <?php
    	require_once "email.class.php";
    	//******************** 配置信息 ********************************
    	$smtpserver = "smtp.mailgun.org";//SMTP服务器
    	$smtpserverport =25;//SMTP服务器端口
    	$smtpusermail = "postmaster@sandbox1444.mailgun.org";//SMTP服务器的用户邮箱
    	$smtpemailto = $_POST['toemail'];//发送给谁
    	$smtpuser = "postmaster";//SMTP服务器的用户帐号
    	$smtppass = "qwe123456";//SMTP服务器的用户密码
    	$mailtitle = $_POST['title'];//邮件主题
    	$mailcontent = "<h1>".$_POST['content']."</h1>";//邮件内容
    	$mailtype = "HTML";//邮件格式（HTML/TXT）,TXT为文本邮件
    	//************************ 配置信息 ****************************
    	$smtp = new smtp($smtpserver,$smtpserverport,true,$smtpuser,$smtppass);//这里面的一个true是表示使用身份验证,否则不使用身份验证.
    	$smtp->debug = false;//是否显示发送的调试信息
    	$state = $smtp->sendmail($smtpemailto, $smtpusermail, $mailtitle, $mailcontent, $mailtype);

    	echo "<div style='width:300px; margin:36px auto;'>";
    	if($state==""){
    		echo "对不起，邮件发送失败！请检查邮箱填写是否有误。";
    		echo "<a href='index.html'>点此返回</a>";
    		exit();
    	}
    	echo "恭喜！邮件发送成功！！";
    	echo "<a href='index.html'>点此返回</a>";
    	echo "</div>";

     ?>

好了，现在来写一个简单的也页面用来发送邮件，复制代码，另存为index.html
        <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=gb2312" />
    <title>Mailgun邮件服务器测试</title>
    </head>
    <body>
    <form action="sendmail.php" method="post">
    	<p>收件人：<input type="text" name="toemail" /></p>
    	<p>标  题：<input type="text" name="title" /></p>
    	<p>内  容：<textarea name="content" cols="50" rows="5"></textarea></p>
    	<p><input type="submit" value="发送"  /></p>
    </form>
    </body>
    </html>

    好了，都做好了，界面就是这个样子，有点丑啊，毕竟我们是用来测试的。我们输入邮箱密码

![QQ截图20140731144508.png](http://upload-images.jianshu.io/upload_images/24022-2fd3563fa19b1524.png)
点击发送，OK，发送成功！
![QQ截图20140731144527.png](http://upload-images.jianshu.io/upload_images/24022-af4d78fedec51df3.png)

打开Google邮箱看一下，收到一封邮件，测试完成
![QQ截图20140731144541.png](http://upload-images.jianshu.io/upload_images/24022-0fa3ece6ecd8566e.png)


重点在我们的发送邮件这一块的配置，这个就是我们在mailgun上得到的发送邮件服务器地址和账号。
![QQ截图20140731144859.png](http://upload-images.jianshu.io/upload_images/24022-78afb5453718fa49.png)
由于没有接收邮件服务器，（截止我写完文章，他们twitter没有回我）估计也没有，所以不能拿Foxmail做测试了，不过没关系，这个简单的phpmail邮件服务器就搭建完成，不知道你看完教程是否已经理解了。
##提示：Mailgun发送给QQ邮箱好像失败 了，我刚才测试了一下，一直没有收到邮件。
