# Clash 代理配置

这是一个完整的 Clash 代理配置项目，包含优化的配置文件和完整的规则集。

## 项目结构

```
├── clash-config.yaml          # 主配置文件
└── rules/                     # 规则文件目录
    ├── Direct.list            # 直连规则
    ├── Global.list            # 全球代理规则
    ├── Proxy.list             # 代理规则
    ├── cn-ip.list             # 中国IP段规则 (20,313条)
    ├── cn.list                # 中国域名规则 (120,964条)
    ├── private.list           # 私有网络规则 (132条)
    └── youtube.list           # YouTube域名规则
```

## 特性

- ✅ **完整的规则集**: 包含超过14万条精确的分流规则
- ✅ **本地化配置**: 所有规则文件本地化，无需网络连接
- ✅ **优化的策略组**: 支持香港、台湾、新加坡、美国等地区节点分组
- ✅ **智能DNS**: 配置了防污染DNS和假IP模式
- ✅ **TUN模式**: 支持透明代理
- ✅ **Web管理**: 集成zashboard管理界面

## 规则来源

- **中国IP段**: [Loyalsoldier/clash-rules](https://github.com/Loyalsoldier/clash-rules) - 基于17mon数据
- **中国域名**: [Loyalsoldier/clash-rules](https://github.com/Loyalsoldier/clash-rules) - 直连域名规则
- **YouTube规则**: [snapei/clash-pro-rules](https://github.com/snapei/clash-pro-rules)
- **私有网络**: [Loyalsoldier/clash-rules](https://github.com/Loyalsoldier/clash-rules) - 本地网络规则

## 使用方法

1. **下载配置文件**
   ```bash
   git clone https://github.com/jackcsq/clash-config.git
   cd clash-config
   ```

2. **修改机场订阅**
   编辑 `clash-config.yaml` 文件中的 `proxy-providers` 部分，替换为你的机场订阅地址：
   ```yaml
   proxy-providers:
     机场名1:
       url: "你的机场订阅地址"
   ```

3. **启动Clash**
   ```bash
   clash -f clash-config.yaml
   ```

4. **访问管理界面**
   打开浏览器访问: http://localhost:9090/ui
   密码: `123456`

## 配置说明

### 端口配置
- HTTP代理: 7890
- SOCKS5代理: 7891
- 混合代理: 7893
- 管理界面: 9090
- DNS服务: 7874

### 策略组
- **国内**: 直连访问中国网站和服务
- **国外**: 代理访问国外网站
- **YouTube**: 专门的YouTube代理策略
- **其他**: 其他未匹配流量的处理

### 规则优先级
1. YouTube服务 → YouTube策略组
2. 私有网络 → 直连
3. 中国域名 → 直连
4. 中国IP段 → 直连
5. 直连规则 → 直连
6. 代理规则 → 代理
7. 全球规则 → 代理
8. 其他流量 → 其他策略组

## 更新规则

规则文件会定期更新，你可以通过以下方式获取最新规则：

```bash
# 更新中国IP段
curl -o rules/cn-ip.list https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/cncidr.txt

# 更新中国域名
curl -o rules/cn.list https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/direct.txt

# 更新私有网络规则
curl -o rules/private.list https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/private.txt

# 更新YouTube规则
curl -o rules/youtube.list https://raw.githubusercontent.com/snapei/clash-pro-rules/release/youtube.txt
```

## 注意事项

- 请确保你的Clash版本支持 `rule-providers` 功能
- 首次使用前请修改机场订阅地址
- 建议定期更新规则文件以获得最佳体验
- 如需自定义规则，请参考Clash官方文档

## 许可证

MIT License

## 贡献

欢迎提交Issue和Pull Request来改进这个配置。
