# 云原生 SRE 学习路线（全职版 · 2026）

> **定位**：零基础有入门基础 → 云原生 SRE / Kubernetes 工程师
> **节奏**：全职 40+ 小时/周，总周期约 **7-9 个月**
> **核心方法**：官方文档精读 + 动手实验 + 项目驱动，视频仅作补充
> **终点能力**：独立维护生产级 K8s 集群、建设可观测性、落地 CI/CD 与 SRE 实践，并能结合 AI 做智能运维与模型推理服务部署

---

## 一、学习理念与方法论（务必先读）

### 1. 为什么优先文档而非视频

| 维度 | 官方文档 | 视频课 |
|------|---------|--------|
| 准确性 | ★★★★★ 权威、最新 | ★★★ 常滞后半年 - 1 年 |
| 深度 | ★★★★★ 有完整边界说明 | ★★ 偏展示性 |
| 效率 | ★★★★★ 可跳读、搜索 | ★ 线性、倍速仍慢 |
| 检索性 | ★★★★★ 未来随时回查 | ★ 很难找到某一分钟 |

**结论**：视频用来"破冰"（第一次接触某概念时），真正掌握必须靠文档 + 敲命令。

### 2. 每个技术点的学习"四步法"

1. **Why**：这个东西解决了什么问题？没有它会怎样？（读架构综述、对比文章）
2. **How**：官方文档通读一遍架构/核心概念章节（不求细节全懂）
3. **Do**：跟着 quickstart 动手部署一个最小可用系统
4. **Break & Fix**：故意搞坏它（删 Pod、断网、填满磁盘），观察现象并修复

**核心原则**：不要追求"看完"，要追求"我能不看文档复现"。

### 3. 笔记与输出

- 每个阶段结束写一篇**技术博客/自述文档**，逼自己讲清楚
- 所有命令、配置都记录到自己的 Git 仓库（推荐 GitHub 上建 `sre-notes` 仓库）
- 每周末做 **故障演练日**：随机破坏环境并复原

### 4. 环境准备

- **主力机**：一台 16G+ 内存 Linux/Mac，或 Win + WSL2
- **虚拟化**：KVM（Linux 原生）或 VMware/VirtualBox
- **云资源预算**：阿里云/腾讯云学生机或按量付费 100-300 元/月（做 K8s 集群练习用）
- **必备工具**：Git、VSCode（装 Remote-SSH 插件）、tmux、直接学会用 Vim 基础编辑

---

## 二、路线总览（时间表）

| 阶段 | 主题 | 周数 | 累计 |
|------|------|------|------|
| 0 | 准备与工具链 | 1 | 1 |
| 1 | Linux 深度掌握 | 4 | 5 |
| 2 | 编程能力（Python + Go） | 6 | 11 |
| 3 | 网络与 Web 服务 | 2 | 13 |
| 4 | 数据库基础 | 3 | 16 |
| 5 | 容器技术（Docker/Containerd） | 2 | 18 |
| 6 | **Kubernetes 核心**（重中之重） | 8 | 26 |
| 7 | 可观测性体系 | 3 | 29 |
| 8 | CI/CD 与 GitOps | 2 | 31 |
| 9 | IaC 与云平台 | 3 | 34 |
| 10 | SRE 工程理念与实战 | 2 | 36 |
| 11 | AI + 运维结合（结合你的 ML 背景） | 4 | 40 |

**每阶段 = 学 + 敲 + 小项目**，不要"学完再动手"。

---

## 三、各阶段详解

### 阶段 0：准备与工具链（1 周）

#### 目标
建立终身受用的工作流：Git、SSH、Vim、tmux、Markdown。

#### 学什么

| 主题 | 推荐资源 | 方式 |
|------|----------|------|
| Git 深入 | [Pro Git 中文版](https://git-scm.com/book/zh/v2)（免费官方书） | **读前 5 章 + 每条命令都敲** |
| SSH & 密钥 | `man ssh`、`man ssh-config` | 配置免密登录到至少两台机器 |
| Vim 基础 | [vim-adventures.com](https://vim-adventures.com)（前 3 关足够） + `vimtutor` | 玩通关 |
| tmux | [tmux cheatsheet](https://tmuxcheatsheet.com) | 新建/切分窗格/detach 练 20 次 |
| Markdown | CommonMark Spec | 用 md 写第一篇学习笔记 |

#### 产出
- GitHub 账号，开好 `sre-notes` 仓库，写第一个 README
- `.ssh/config`、`.vimrc`、`.tmux.conf` 三份个人配置文件

---

### 阶段 1：Linux 深度掌握（4 周）

#### 目标
不只是会用命令，要理解**为什么是这样**——文件系统、进程、权限、内核、网络栈。

#### Week 1-2：系统与 Shell

| 主题 | 推荐资源 | 方式 |
|------|----------|------|
| 系统原理 | 📘 **《鸟哥的 Linux 私房菜·基础学习篇》（第四版）** | 精读第 5-20 章，每一节的命令**全部敲一遍** |
| Shell 脚本 | 📘 **《Linux Command Line and Shell Scripting Bible》** | 边读边写，完成 [bash-scripting challenges](https://github.com/bobbyiliev/101-bash-commands) |
| 权限 & 特殊位 | `man chmod`、`man setuid` | 动手创建 setuid 场景并分析 |
| 包管理 | `apt`/`dnf`/`rpm` 官方文档 | 编译一个源码包安装（如 nginx） |

#### Week 3：进程、内存、内核

| 主题 | 资源 | 方式 |
|------|------|------|
| 进程/线程/信号 | 📘 **《Linux 性能优化实战》倪朋飞**（极客时间，有文字版） | 看前 15 讲，每讲都在自己机器上复现 |
| 内存管理 | 同上 + `free`、`vmstat`、`/proc/meminfo` | 写一个吃内存脚本观察 OOM Killer |
| 文件系统 | `man ext4`、`lsblk`、`mount` 官方 | 自己挂载一个 loop device |
| systemd | [systemd 官方文档](https://www.freedesktop.org/wiki/Software/systemd/) | 写两个自定义 service 单元 |

#### Week 4：Linux 网络与排障

| 主题 | 资源 | 方式 |
|------|------|------|
| 网络基础 | 📘 **《TCP/IP 详解 卷一》第 1-6 章**（经典必读） | 抓包复现三次握手 |
| 工具链 | `tcpdump`、`ss`、`ip`、`nmap`、`iperf3` 的 man page | 给自己写一个 10 条命令的 cheatsheet |
| iptables/nftables | [netfilter 官方 wiki](https://netfilter.org/) | 手写一套防火墙规则 |
| 故障排查 | 📘 **《性能之巅 (BPF Performance Tools)》by Brendan Gregg** 前 4 章 | 用 `perf`、`strace`、`bpftrace` 排查一次慢进程 |

#### 阶段 1 产出（必做）
1. **项目**：从零在一台 Ubuntu Server 上手动搭建 LAMP/LNMP 环境（不用 apt 一键安装，源码编译）
2. **博客**：写一篇《Linux 进程与 systemd 的关系》
3. **脚本集**：10 个实用 shell 脚本（备份、日志分析、批量 ping 等）

---

### 阶段 2：编程能力 —— Python + Go（6 周）

> **重点强调**：这是马哥路线最大的短板，但却是 SRE 的分水岭。**只会 Shell 的是运维，会 Python+Go 的才是 SRE**。

#### Week 5-7：Python 进阶（你已有基础，加速）

| 主题 | 资源 | 方式 |
|------|------|------|
| 现代 Python | 📘 **《流畅的 Python》(Fluent Python) 第二版** | 重点读第 1-10 章、15-20 章 |
| 官方教程 | [docs.python.org/3/tutorial](https://docs.python.org/3/tutorial/) | 过一遍查漏补缺 |
| 异步编程 | `asyncio` 官方文档 | 写一个并发 HTTP 探测工具 |
| 网络编程 | `requests`、`httpx`、`paramiko` | 写一个批量跑机器命令的小工具 |
| API 框架 | **FastAPI** 官方文档 | 写一个"主机信息查询"API |
| 测试 | `pytest` 官方文档 | 给上面的工具补单测 |

#### Week 8-10：Go 入门到实战（SRE 必备）

> Kubernetes、Prometheus、Docker、etcd、Terraform 全是 Go 写的。不懂 Go，云原生底层源码就是黑盒。

| 主题 | 资源 | 方式 |
|------|------|------|
| 语法 | [A Tour of Go](https://go.dev/tour/) | 全过一遍，所有练习都做 |
| 官方文档 | [Effective Go](https://go.dev/doc/effective_go) | 精读 |
| 书 | 📘 **《Go 语言圣经》(The Go Programming Language) by Donovan & Kernighan** | 过 1-8 章 |
| 并发 | `sync`、`context`、channel 官方文档 | 写一个并发 worker pool |
| 网络/HTTP | `net/http` 官方 | 写一个类似 httpbin 的服务 |
| CLI 工具 | `cobra` + `viper` 官方文档 | 写一个自己的 `kubectl`-like CLI |

#### 阶段 2 产出
- **Python 项目**：一个小型运维平台（主机管理、命令批量执行、Web UI）
- **Go 项目**：仿一个 `ping`/`nslookup` 的命令行工具，含单测、打包到 `releases`
- 开始养成看 K8s/Prometheus 源码的习惯（哪怕只看 `README` 和 `main.go`）

---

### 阶段 3：网络与 Web 服务（2 周）

#### Week 11：协议与 Web 服务器

| 主题 | 资源 | 方式 |
|------|------|------|
| HTTP/1.1 & HTTP/2 & HTTP/3 | [MDN HTTP 指南](https://developer.mozilla.org/zh-CN/docs/Web/HTTP) | 读完 + 用 curl 观察头部 |
| TLS/HTTPS | Let's Encrypt 官方文档 | 给一个自建域名申请证书并部署 |
| Nginx | [Nginx 官方文档](http://nginx.org/en/docs/) | 配置反向代理 + 负载均衡 + 静态加速 |
| 高级 Nginx | 📘 **《Nginx 高性能 Web 服务器详解》** | 写一份限流 + 缓存的 nginx.conf |

#### Week 12：负载均衡与 DNS

| 主题 | 资源 | 方式 |
|------|------|------|
| LVS/HAProxy | 官方文档 | 搭建 4 层 + 7 层双负载均衡 |
| Keepalived | 官方文档 | 实现两台 nginx 主备漂移 |
| DNS | `dig`/`nslookup` + BIND 官方 | 搭建内网 DNS 服务器 |

> 说明：云原生时代 LVS/Keepalived 使用减少，但求职面试仍高频考，过一遍即可，不需深入。

#### 阶段 3 产出
- 一套自建网站（自己域名 + HTTPS + 反代 + 限流）部署文档

---

### 阶段 4：数据库（3 周）

#### Week 13：MySQL

| 主题 | 资源 | 方式 |
|------|------|------|
| SQL 基础 | MySQL 官方手册 | 刷 [SQLZoo](https://sqlzoo.net/) + LeetCode Database 前 30 题 |
| 原理 | 📘 **《MySQL 45 讲》林晓斌**（极客时间） | 至少看完前 25 讲 |
| 主从复制 | MySQL 官方 Replication 章节 | 搭一主两从 |
| 慢查询优化 | `EXPLAIN`、索引原理 | 造 100 万条数据分析执行计划 |

#### Week 14：PostgreSQL（马哥路线缺失，但越来越重要）

| 主题 | 资源 | 方式 |
|------|------|------|
| PostgreSQL | [官方文档](https://www.postgresql.org/docs/) | 搭一套 + 对比 MySQL 差异 |
| 备份/恢复 | pg_dump、pg_basebackup | 模拟灾难恢复 |

#### Week 15：Redis + 其他

| 主题 | 资源 | 方式 |
|------|------|------|
| Redis | [Redis 官方文档](https://redis.io/docs/)、📘 **《Redis 设计与实现》黄健宏** | 过一遍数据结构 + 搭建 Cluster |
| 扫盲 | MongoDB、ClickHouse、Etcd 各 1 天 | 仅了解定位和适用场景 |

#### 阶段 4 产出
- 一份《主流数据库对比选型文档》
- 搭建并跑通 MySQL 主从 + Redis Cluster + 一个写入压测

---

### 阶段 5：容器技术（2 周）

#### Week 16：Docker

| 主题 | 资源 | 方式 |
|------|------|------|
| 核心概念 | [Docker 官方文档](https://docs.docker.com/) | 读完 "Get started" 全部章节 |
| 原理 | namespace、cgroup（📘《自己动手写 Docker》陈显鹭，短但精） | 用 Go 写个 mini-docker |
| Dockerfile | 官方 best practices | 写 5 个不同语言的 Dockerfile 并优化体积 |
| 网络与存储 | 官方文档 | 实现容器间通信的 3 种方式 |
| Compose | 官方 | 用 compose 拉起 WordPress/GitLab |

#### Week 17：Containerd、Harbor

| 主题 | 资源 | 方式 |
|------|------|------|
| Containerd | [官方文档](https://containerd.io/docs/) | 纯 containerd 运行容器（`ctr`、`nerdctl`） |
| 镜像仓库 | Harbor 官方文档 | 搭一套私有 Harbor + 推拉 |
| 镜像安全 | Trivy 官方 | 扫描自己的镜像并修漏洞 |

#### 阶段 5 产出
- 一个多阶段构建、体积 < 50MB 的 Go 应用镜像
- 自建 Harbor 仓库 + CI 推送流程雏形

---

### 阶段 6：Kubernetes —— 核心主战场（8 周）

> **这是整个路线 ROI 最高的 8 周**。不懂 K8s 就不是云原生 SRE。

#### Week 18-19：K8s 入门

| 主题 | 资源 | 方式 |
|------|------|------|
| 总览 | 📘 **《Kubernetes 权威指南》第 6 版** or 📘 **《Kubernetes in Action》(中译本)** | 精读前 5 章 |
| 官方教程 | [kubernetes.io/docs/tutorials](https://kubernetes.io/docs/tutorials/) | **全部跑一遍** |
| 本地环境 | kind / minikube / k3s | 三个都装一遍，熟悉差异 |
| 核心概念 | Pod、Service、Deployment、ConfigMap | 每个对象手写 YAML 不抄不复制 |

#### Week 20-21：进阶对象与调度

| 主题 | 资源 | 方式 |
|------|------|------|
| Workload | StatefulSet、DaemonSet、Job、CronJob | 各部署一次有状态应用 |
| 存储 | PV/PVC/StorageClass 官方 | 搭建 NFS 动态供给 |
| 网络 | Service 类型、Ingress、NetworkPolicy | 安装 Ingress-Nginx + 配 TLS |
| 调度 | 亲和性/反亲和性/污点容忍 | 写 5 种调度约束并验证 |

#### Week 22-23：集群运维

| 主题 | 资源 | 方式 |
|------|------|------|
| 手动部署集群 | [kubeadm 官方](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/) | 3 节点集群（1 master + 2 worker） |
| 源码级部署 | [kelseyhightower/kubernetes-the-hard-way](https://github.com/kelseyhightower/kubernetes-the-hard-way) | **必做，一次打通所有组件** |
| 认证与授权 | RBAC、ServiceAccount 官方 | 给三种角色创建不同权限 |
| Helm | Helm 官方文档 | 打包自己的应用为 Chart |
| Operator | kubebuilder 官方文档 | 用 Go 写一个 Hello-Operator |

#### Week 24-25：深入 & 考证

| 主题 | 资源 | 方式 |
|------|------|------|
| CNI/CSI/CRI | Calico、Cilium、longhorn 官方 | 至少深入一个 CNI（推 Cilium） |
| eBPF 初探 | [ebpf.io/learn](https://ebpf.io/learning/) | 看懂 Cilium 大致原理 |
| 故障排查 | 📘 **《Kubernetes Patterns》** + 📘 **《Production Kubernetes》** | 精读 |
| **CKA 认证** | [CNCF CKA](https://www.cncf.io/certification/cka/) + [killer.sh](https://killer.sh) 模拟器 | **建议本阶段末报名考 CKA** |

#### 阶段 6 产出
- 3 节点生产级 K8s 集群一套（含 Ingress、存储、监控雏形）
- 一个自己写的 Operator（能 reconcile 自定义资源）
- **CKA 证书**（强烈推荐，简历加分）

---

### 阶段 7：可观测性体系（3 周）

> **可观测性 = Metrics + Logs + Traces**。这是 SRE 的眼睛和耳朵。

#### Week 26：Metrics（Prometheus 系）

| 主题 | 资源 | 方式 |
|------|------|------|
| Prometheus | [官方文档](https://prometheus.io/docs/) | 搭建 + 写 10 条 PromQL |
| Grafana | 官方文档 | 做 3 个自用 Dashboard |
| Alertmanager | 官方文档 | 配钉钉/飞书告警 |
| kube-prometheus-stack | GitHub 仓库 | 在 K8s 里一键装好 |

#### Week 27：Logs + Traces

| 主题 | 资源 | 方式 |
|------|------|------|
| Loki | Grafana Loki 官方 | 替代 ELK 做日志聚合 |
| ELK（扫盲） | ES + Filebeat + Kibana 官方 | 搭一套理解经典方案 |
| OpenTelemetry | [opentelemetry.io](https://opentelemetry.io/docs/) | 给一个 FastAPI 应用打点 |
| Jaeger/Tempo | 官方 | 链路追踪一次完整请求 |

#### Week 28：生产级实战

| 主题 | 资源 | 方式 |
|------|------|------|
| SLI/SLO 实践 | 📘 **Google《Site Reliability Engineering》第 4 章** | 给一个服务设计 SLO + Error Budget |
| 告警降噪 | PromQL + 分组/抑制规则 | 写一套生产级告警规则 |

#### 阶段 7 产出
- 一套完整的 K8s 可观测性方案：Prometheus + Grafana + Loki + Tempo + OpenTelemetry，全部有自定义 Dashboard

---

### 阶段 8：CI/CD 与 GitOps（2 周）

> **重要更新**：现代 SRE 用 GitOps 多于传统 Jenkins。两者都要会，重点 GitOps。

#### Week 29：传统 CI/CD

| 主题 | 资源 | 方式 |
|------|------|------|
| Git 工作流 | GitHub Flow / GitFlow | 实操 feature-branch + PR review |
| GitHub Actions | [官方文档](https://docs.github.com/actions) | 给自己项目写一个完整流水线 |
| GitLab CI | GitLab 官方 | 搭自建 GitLab + Runner |
| Jenkins（次要）| 官方 | 过一遍流水线写法即可 |

#### Week 30：GitOps（现代派，重点）

| 主题 | 资源 | 方式 |
|------|------|------|
| ArgoCD | [ArgoCD 官方](https://argo-cd.readthedocs.io/) | 部署一个完整 GitOps 流程 |
| Flux（了解）| 官方 | 对比 ArgoCD |
| 镜像扫描 | Trivy、Cosign | 加入流水线 |

#### 阶段 8 产出
- 完整 DevOps 链路：代码提交 → GitHub Actions 构建 → 推 Harbor → ArgoCD 自动发布到 K8s

---

### 阶段 9：IaC 与云平台（3 周）

#### Week 31-32：Terraform + 云

| 主题 | 资源 | 方式 |
|------|------|------|
| Terraform | [官方文档](https://developer.hashicorp.com/terraform) + [Learn Terraform](https://developer.hashicorp.com/terraform/tutorials) | 用 tf 创建完整 VPC + K8s 集群 |
| 阿里云 ACK / 腾讯云 TKE | 官方文档 | 用 tf 一键拉起托管 K8s |
| AWS/GCP（了解） | 官方 | 跑一遍 EKS/GKE 快速开始 |

#### Week 33：配置管理

| 主题 | 资源 | 方式 |
|------|------|------|
| Ansible | [官方文档](https://docs.ansible.com/) | 写 10 个 Role 自动化常见任务 |
| Packer | 官方文档 | 构建自定义镜像 |

#### 阶段 9 产出
- 一套 Terraform 模块：一键拉起阿里云 VPC + ACK + RDS + Redis 的完整环境

---

### 阶段 10：SRE 工程理念与实战（2 周）

> 这里是区分"会用工具的运维"和"真正的 SRE"的分水岭。

#### Week 34：三本 SRE 圣经

| 书目 | 精读重点 |
|------|----------|
| 📘 **《Site Reliability Engineering》** (Google, 免费在线) | 第 1-6 章、12-18 章 |
| 📘 **《The Site Reliability Workbook》** (Google, 免费) | SLI/SLO 章节 |
| 📘 **《Seeking SRE》** | 选读 |

在线链接：[sre.google/books](https://sre.google/books/)

#### Week 35：实战

| 主题 | 方式 |
|------|------|
| Postmortem 文化 | 选一个公开故障复盘（如 GitLab、Cloudflare 的），自己写一份 |
| Chaos Engineering | 装 Chaos Mesh，故意注入故障到 K8s，观察监控和告警 |
| Capacity Planning | 给一个服务做容量评估 |

#### 阶段 10 产出
- 一篇自己主导的"故障演练报告"
- 一份 SLI/SLO 设计文档

---

### 阶段 11：AI + 运维结合（4 周）· 结合你的 object_detection 背景

> 你已有 ML 基础，这里把 AI 和 SRE 打通，打造差异化竞争力。

#### Week 36-37：MLOps 基础

| 主题 | 资源 | 方式 |
|------|------|------|
| MLOps 概念 | [ml-ops.org](https://ml-ops.org/)、[Made With ML](https://madewithml.com/) | 理解生命周期 |
| 模型部署 | BentoML / KServe 官方 | 把你的 object_detection 模型打包为在线服务 |
| 模型监控 | Evidently AI 官方 | 监控模型漂移 |
| 实验管理 | MLflow 官方 | 跑通一次实验追踪 |

#### Week 38：大模型服务化

| 主题 | 资源 | 方式 |
|------|------|------|
| LLM 推理 | vLLM / Ollama 官方 | 本地部署 DeepSeek / Qwen 模型 |
| K8s 上的 GPU 调度 | NVIDIA Device Plugin 官方 | GPU 集群调度 |
| LLM 观测 | Langfuse / OpenLLMetry | 给 LLM 应用加观测 |

#### Week 39：AIOps 实战

| 主题 | 方式 |
|------|------|
| 日志异常检测 | 用 Python + sklearn 对日志做聚类异常检测 |
| LLM 告警降噪 | 用 LangChain + DeepSeek API 做告警归并/根因推断 Demo |
| RAG on Ops | 把公司 wiki + runbook 喂给 RAG，做一个值班助手 |

#### 阶段 11 产出
- **差异化项目**：《基于 DeepSeek 的智能值班助手》——RAG + 告警归并 + 根因分析
- **融合项目**：把 object_detection 模型部署到 K8s 上，完整带 Prometheus 指标、HPA 自动扩容、灰度发布

---

## 四、关键里程碑项目（阶段性考核）

| 里程碑 | 时间点 | 能讲清楚它就证明你达标 |
|--------|--------|-------------------------|
| M1 | 第 4 周 | 手动编译源码部署一个 LNMP 并说清每一步原因 |
| M2 | 第 10 周 | 用 Go 实现的 CLI 工具有 > 5 个子命令 + 单测覆盖 |
| M3 | 第 17 周 | 用 Terraform + Ansible 一键搭建一套 Web 架构 |
| M4 | 第 25 周 | 通过 CKA 考试 |
| M5 | 第 30 周 | 完整 GitOps 链路，提交代码 5 分钟内自动上线 |
| M6 | 第 35 周 | 在生产级 K8s 上做一次 Chaos 故障演练并写复盘 |
| M7 | 第 40 周 | 交付 AI+SRE 融合项目，能在面试中讲 20 分钟 |

---

## 五、推荐书单（按优先级）

**必读（★★★★★）**
1. 《鸟哥的 Linux 私房菜·基础学习篇》第四版
2. 《Linux 性能优化实战》倪朋飞
3. 《TCP/IP 详解 卷一》
4. 《Kubernetes 权威指南》第 6 版 或 《Kubernetes in Action》
5. Google 《Site Reliability Engineering》+ 《Workbook》（免费在线）
6. 《流畅的 Python》
7. 《Go 语言圣经》

**进阶（★★★★）**
- 《MySQL 45 讲》林晓斌
- 《BPF Performance Tools》Brendan Gregg
- 《Production Kubernetes》
- 《Designing Data-Intensive Applications》（DDIA）

**查漏补缺（★★★）**
- 《Pro Git》
- 《Effective Python》
- 《The Pragmatic Programmer》

---

## 六、证书建议（按 ROI 排序）

| 证书 | 必要性 | 成本 | 备考时间 |
|------|--------|------|----------|
| **CKA** | ★★★★★ 强烈推荐 | ~$400 | 2 周（已学完 K8s 后） |
| CKS（K8s 安全） | ★★★★ 进阶推荐 | ~$400 | 2 周 |
| CKAD | ★★★ 偏开发 | ~$400 | 1 周 |
| 云厂商证书（阿里 ACP / AWS SAA）| ★★★ | ¥1200 / $150 | 3-4 周 |
| RHCE | ★★ 传统运维导向 | 较贵 | 不建议 |

---

## 七、求职与面试准备

### 简历亮点（按此路线结业后可写）
1. 独立搭建生产级 K8s 集群，含 Calico/Cilium CNI、Longhorn 存储
2. CKA 认证
3. 开发过 K8s Operator（加分项，很多人没有）
4. 全套可观测性方案（Prom + Grafana + Loki + OTel）
5. AI+SRE 项目：基于 DeepSeek 的智能运维助手

### 重点面试考点
- Linux：IO 模型、OOM、文件描述符、TCP 握手挥手
- K8s：Pod 调度流程、Service 背后的 iptables/IPVS、Controller 原理
- Prometheus：PromQL、rate() vs irate()、Pull 模型为什么不用 Push
- 故障排查：一个 Pod 起不来你怎么排？（必考）

### 模拟面试资源
- [interviewing.io](https://interviewing.io/)
- 《剑指 Offer》+ 力扣 Top 100（基础编程题仍会考）

---

## 八、关键建议 & 避坑指南

1. **不要贪多**：每个工具先会用再懂原理再看源码，别一上来啃源码
2. **别停在"看"**：每个 YAML/配置/命令都要自己敲，**看 10 遍不如敲 1 遍**
3. **博客/GitHub 动起来**：招聘时一个活跃的 GitHub 比十份简历还管用
4. **英文文档习惯**：K8s/Prometheus/CNCF 生态最新信息 90% 在英文，**马上开始用英文版官方文档**
5. **不要陷入工具海**：Service Mesh（Istio）、Serverless、eBPF 深度等都是后话，先把核心主线走完
6. **AI 部分别学太早**：一定要先把 K8s 和可观测性打牢，再搞 AI 结合，否则 AI 加上去是空中楼阁
7. **每月复盘**：第 4、8、12... 周末做一次总复盘，回看笔记、调整节奏
8. **加入社区**：CNCF Slack、K8s 中文社区、公众号「云原生实验室」、GitHub trending

---

## 九、全局进度追踪表（自己维护）

```
□ 阶段 0  准备工具链           Week 1
□ 阶段 1  Linux 深度            Week 2-5
□ 阶段 2  Python + Go           Week 6-11
□ 阶段 3  网络 & Web            Week 12-13
□ 阶段 4  数据库                Week 14-16
□ 阶段 5  容器                  Week 17-18
□ 阶段 6  Kubernetes            Week 19-26 ★ CKA
□ 阶段 7  可观测性              Week 27-29
□ 阶段 8  CI/CD + GitOps        Week 30-31
□ 阶段 9  IaC + 云平台          Week 32-34
□ 阶段 10 SRE 理念              Week 35-36
□ 阶段 11 AI + 运维             Week 37-40
```

---

## 十、结语

这条路线**比马哥路线更硬核、更现代、也更累**。好处是：
- 你学完不是"标准运维"，而是真正的**云原生 SRE**
- 结合 object_detection 背景，你在 AI 运维方向有独特优势
- 全部是公开免费资源（零培训费）

**开工建议**：今天把阶段 0 的 GitHub 仓库建起来，写第一篇 README，明天就开始阶段 1 的 Week 1。

**最后一句话**：不要完美主义地"准备好再开始"，**开始即完美**。

---

> 文件创建于 2026-04-20
> 路线基于你的目标：云原生 SRE / K8s 工程师，全职学习节奏
> 建议每 4 周回来复盘一次，调整节奏
