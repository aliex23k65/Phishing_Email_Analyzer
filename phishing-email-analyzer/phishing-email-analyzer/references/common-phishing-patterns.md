# FS.COM 常见钓鱼模式案例库

本文档整理了 FS.COM 销售团队最常遭遇的钓鱼攻击模式，按威胁等级和出现频率排序。
分析邮件时可参考这些模式进行模式匹配，提高识别准确度。

---

## 模式一：附件钓鱼登录陷阱（出现频率：极高）

### 攻击特征

- 邮件附带 .html、.htm 或 .zip（解压后是 .html）文件
- 文件名通常伪装成业务文档：BOM表、报价单、PI、Data Sheet、合规认证等
- 打开后显示模糊的文档预览 + 登录弹窗（Google / Microsoft 365 / 公司 SSO）
- 声称"文件已加密"或"需要验证身份才能查看"

### 常见伪装名称

- `BOM_Q2_2026_Updated.html`
- `PO-Confirmation-FS2026.htm`
- `DataSheet-400G-QSFP-DD.html`
- `Compliance-Certificate.zip`（解压后是 .html）
- `Shared-Document-View.html`
- `Invoice_Payment_Details.htm`

### 识别要点

- 正常的 BOM/报价单是 .xlsx、.csv 或 .pdf，不会是 .html
- 正常的业务文件打开就能看，不需要输入任何账号密码
- 登录弹窗的 URL 不是 accounts.google.com 或 login.microsoftonline.com

### 真实案例模式

```
邮件主题：Re: Urgent - Updated BOM List for Q2 Order
附件：BOM_Q2_2026_Updated.html
话术："The file is password-protected for security"
陷阱：打开后显示模糊表格 + Google 登录弹窗
```

---

## 模式二：支付重定向 / BEC 欺诈（出现频率：高，危害最大）

### 攻击特征

- 冒充已知客户或供应商，声称变更收款银行账号
- 通常在交易即将付款的关键节点出现
- Reply-to 地址与 From 地址不一致（常指向 Gmail/Outlook 等免费邮箱）
- 收款公司名称与发件公司名称有细微差异
- 常用借口：银行系统升级、审计要求、公司重组

### 常见话术

- "Our company has recently changed our banking partner"
- "Due to a system upgrade, please update our payment details"
- "The old account will be deactivated by end of this week"
- "Please process the payment to the new account as soon as possible"
- "银行系统维护，临时变更收款路径"

### 识别要点

- 检查 Reply-to 是否与 From 一致
- 收款公司名称是否与发件公司完全一致
- 正规的银行账号变更应有盖章的银行证明文件
- 任何收款变更都必须通过官网电话二次确认

### 真实案例模式

```
From: jennifer.w@globalnetwork-inc.com
Reply-to: jennifer.williams.finance@gmail.com  ← 红旗！
主题：URGENT: Bank Account Change
话术："bank system upgrade" + "old account deactivated this week"
陷阱：新收款账号指向攻击者控制的账户
```

---

## 模式三：Adobe/Microsoft 品牌仿冒（出现频率：高）

### 攻击特征

- 伪装成 Adobe Acrobat Sign、Adobe Document Cloud、Microsoft SharePoint 的通知邮件
- 声称有文档需要签署或查看
- 点击后跳转到仿冒的登录页面
- 页面设计高度模仿官方，普通用户难以分辨

### 常见伪装主题

- "You have a document to sign via Adobe Sign"
- "Shared document: Purchase Order #FS-2026-XXX"
- "[Company Name] shared a file with you via SharePoint"
- "Action Required: Review and sign the attached contract"

### 识别要点

- 检查发件人是否来自 @adobe.com 或 @microsoft.com 官方域名
- 链接的真实域名是否是 adobe.com / microsoft.com / sharepoint.com
- Adobe Sign 的真实通知来自 adobesign@adobesign.com
- 如果不确定，不要点击邮件中的链接，直接登录对应平台查看是否有待处理文档

---

## 模式四：OAuth 授权劫持（出现频率：中，隐蔽性极高）

### 攻击特征

- 不要求你输入密码，而是诱导你点击"允许/Authorize"按钮
- 授权一个恶意的第三方应用访问你的 Google/Microsoft 账号
- 一旦授权，攻击者可以读取你的邮件、联系人，甚至代你发邮件
- 即使你之后改了密码，授权仍然有效（除非手动撤销）

### 常见话术

- "Please authorize access to view the shared document"
- "Click Allow to continue"
- "Grant permission to access your files"

### 识别要点

- 正常的文档分享不需要你授权第三方应用
- 如果看到"此应用想要访问你的邮件/联系人"的权限请求，立即关闭
- 检查 Google 账号安全设置中的"第三方应用访问权限"，撤销不认识的应用

---

## 模式五：鱼叉式钓鱼 / 定向攻击（出现频率：中低，精准度高）

### 攻击特征

- 攻击者事先调查了目标（通过 LinkedIn、公司官网、社交媒体等）
- 邮件内容高度个性化，提到你的真实姓名、职位、最近的项目或展会
- 可能冒充你的同事、上级或合作伙伴
- 内容看起来非常合理，难以通过常规特征识别

### 识别要点

- 即使邮件内容看起来很合理，也要检查发件域名是否正确
- 涉及敏感操作（转账、提供凭据、下载文件）时，通过其他渠道确认
- 注意"差一点"的域名：fs-com.co、fscorn.com、fs.com.cn（如果不是官方域名）

---

## 模式六：克隆钓鱼（出现频率：低，迷惑性极高）

### 攻击特征

- 攻击者复制一封你之前收到过的真实邮件
- 替换其中的链接或附件为恶意版本
- 声称"之前的链接有问题，这是更新版"或"附件已更新"
- 因为邮件内容你之前见过，警惕性会大幅降低

### 识别要点

- 如果收到"更新版"邮件，对比发件地址是否与之前完全一致
- 检查链接是否与之前的版本不同
- 通过其他渠道确认对方是否真的发了更新版

---

## 快速判断清单（给销售同事的速查表）

遇到可疑邮件时，快速过一遍这 5 个问题：

1. ❓ 附件是 .html 文件，或者打开后要我输入密码？→ 几乎肯定是钓鱼
2. ❓ 要求变更收款银行账号？→ 必须通过官网电话确认，不能只凭邮件
3. ❓ Reply-to 地址跟发件人不一样？→ 高度可疑
4. ❓ 催我"今天必须处理"但我之前没听说过这件事？→ 可能是制造紧迫感的话术
5. ❓ 让我点链接登录或授权某个应用？→ 不要点，手动去官网操作
