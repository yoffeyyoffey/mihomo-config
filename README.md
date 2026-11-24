# mihomo-config

个人 **FlClash / mihomo** 网络分流配置管理与学习工程（Configuration as Code）。

## 安全原则（必读）

- **`local/` 目录已被 `.gitignore` 严格忽略**：里面存放包含真实 VPS IP、UUID、密码的原始可用配置，**绝不会上传到 GitHub**。
- **`templates/` 目录存放脱敏模板**：所有敏感信息已替换为占位符（如 `YOUR_VPS_IP`、`YOUR_VLESS_UUID`），可放心查阅、学习与版本托管。

## 目录结构

```text
D:\project\mihomo-config\
├── local/
│   └── mobile.local.yaml      # 原始可用手机版配置（原样备份，已 gitignore，不上传）
├── templates/
│   └── mobile.example.yaml    # 脱敏学习模板（与原配置结构一致，可安全上传 GitHub）
├── .gitignore                 # 防止敏感配置泄露的安全规则
├── README.md                  # 项目说明与配置模块速查
└── ROADMAP.md                 # 后续学习与扩展计划
```

## 配置文件 6 大模块速查

1. **基础运行参数**（`mixed-port`, `mode: rule`, `external-controller`）：定义本地代理端口与规则分流模式。
2. **流量嗅探**（`sniffer`）：识别 HTTP / TLS / QUIC 连接中的真实域名，提升分流准确度。
3. **DNS 模块**（`dns`）：配置 DoH 加密解析与 `fake-ip`，并用 `fake-ip-filter` 排除局域网和特殊应用。
4. **节点定义**（`proxies`）：配置同一台 VPS 的多种协议通道（VLESS+REALITY、Hysteria2 固定/跳跃/443 等）。
5. **策略组**（`proxy-groups`）：在客户端展示的可切换分组（`PROXY`）。
6. **规则集与分流规则**（`rule-providers` + `rules`）：按**从上到下优先匹配**执行：
   - 校园网 & 私有网络 → `DIRECT`
   - Google & AI 服务 → `PROXY`
   - Steam 大流量下载 → `DIRECT`
   - 广告与追踪 → `REJECT`
   - 常规海外 / Telegram → `PROXY`；国内域名 / 国内 IP → `DIRECT`
   - 兜底规则 `MATCH` → `PROXY`
