CF部署Workers网址导航

1.创建 Workers

2.创建KV空间，KV名称随便

3.绑定KV空间，KV变量名必须与代码中的变量名称一致，有2个版本代码分别有XMTY和NAV_DB版本代码

4.复制js文件里面的代码在CF编辑器中粘贴部署，js文件中//注释掉的文字代码可以不用复制

5.打开网页测试确认成功后，绑定域名，完成。

6.默认密码：admin888


代码会优先读取 KV 密码，只有 KV 中没有保存密码时才使用变量密码，默认一般不需要设置变量密码，如果要设置，变量名称必须是：ADMIN_PASSWORD ，密码可以随便设置

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
