# ROADMAP — mihomo-config

## Phase 1：归档与安全隔离（已完成）
- [x] 在 `D:\project\mihomo-config` 建立独立工程目录
- [x] 原样归档手机版配置至 `local/mobile.local.yaml`（已通过 `.gitignore` 屏蔽）
- [x] 生成脱敏版模板 `templates/mobile.example.yaml`
- [x] 初始化本地 Git 仓库并确认敏感文件不会入库

## Phase 2：吃透原理（待开始）
- [ ] 逐段理解 `sniffer`、`dns`（`fake-ip`）与 `rules` 优先级顺序
- [ ] 尝试添加自定义分流规则（如常用学习/开发网站直连或代理）

## Phase 3：工程化扩展（待开始）
- [ ] 拆分公共规则与多端差异（`mobile.yaml` + `desktop.yaml`）
- [ ] 编写 `scripts/build.py` 自动合并模板与本地密钥，并校验 YAML 语法
- [ ] 关联 GitHub 仓库进行长期版本迭代
