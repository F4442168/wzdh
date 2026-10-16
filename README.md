CF部署Workers网址导航

1.创建 Workers

2.创建KV空间，KV名称随便

3.绑定KV空间，KV变量名必须与代码中的变量名称一致，有2个版本代码分别有XMTY和NAV_DB版本代码

4.复制js文件里面的代码在CF编辑器中粘贴部署，js文件中//注释掉的文字代码可以不用复制,推荐使用XMYT-pro版，代码有优化提升可读性。

5.打开网页测试确认成功后，绑定域名，完成。

6.默认密码：admin888


#代码会优先读取 KV 密码，只有 KV 中没有保存密码时才使用变量密码，默认一般不需要设置变量密码，如果要设置，变量名称必须是：ADMIN_PASSWORD ，密码可以随便设置

要想优先使用变量密码，修改代码，让环境变量优先
在 Worker 代码中找到类似下面的代码：

const adminPwd = await env.NAV_DB.get("adminPwd")

  || env.ADMIN_PASSWORD
  
  || "admin888";

  将它改成：
  
  const adminPwd =
  
  env.ADMIN_PASSWORD ||
  
  await env.NAV_DB.get("adminPwd") ||
  
  "admin888";
  
  这样读取优先级就会变成：

1. ADMIN_PASSWORD Secret变量密码

2. KV 中的 adminPwd

3.以上都没有使用 默认密码： admin888


#原版自定义背景链接地址：https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=80&w=2564&auto=format&fit=crop

#如忘记密码:

默认的后台管理密码是 admin888。登录后可自行修改 如忘记密码 登录 Cloudflare 控制面板。

在左侧菜单栏点击-存储和数据库-> 然后点击workers kv

在列表中，找到你之前创建的那个数据库名称（比如 NAV_DATABASE），点击它进入查看。

再点击-KV对-在下方的数据列表里，你会看到一个名为 site_config 的密钥（Key）。

点击后面的 “下载” ，下载后用记事本打开,或者点编辑查看。

你会看到一段类似于这样的代码：

JSON {"wallpaper":"xxx","dynamicSections":[],"adminPwd":"你忘记的那个密码"}

👉 "adminPwd" 后面的内容就是你的当前密码！ 看完记住它，直接回去登录就行了。
