# 裴奕名 · Yiming Pei

**C++ / Linux 系统编程** · 江汉大学 智能制造工程 2027 届 · 武汉

写系统底层，也写跑在上面的完整应用。下面两个项目从并发模型、资源隔离到部署上线都是我自己做的——代码、测试、CI、设计文档都在仓库里，能点开验证。

`C++11/17` · `Linux 系统调用` · `并发与资源限制` · `MySQL 8` · `AI Agent 协同开发`

---

## 精选项目

### MiniOJ — 在线判题系统

`C++17` `cpp-httplib` `MySQL 8` `Linux` `rlimit 沙箱`

fork/exec 起子进程跑用户代码，进子进程后 `setrlimit` 上三重硬限制，父进程按 wall clock 兜底 kill，8 路评测 worker 由条件变量队列调度，输出六种判定：AC / WA / TLE / MLE / CE / RE。

- **沙箱参数**：CPU 时间 = 题目时限 + 1s（`RLIMIT_CPU`）；虚拟地址空间 = 2 × 内存限制（默认 256MB 题 → 512MB `RLIMIT_AS`，RSS 超限判 MLE）；单次输出 16MB 上限（`RLIMIT_FSIZE`）；编译超时 3s，默认测例时限 500ms
- 子进程 stdin / stdout 走管道全量 drain，读端不被用户程序的输出阻塞；并发评测靠 worker 队列而不是每请求 fork
- 实测 200 并发提交 P95 判题 1.4s，队列满时排队而非拒绝
- 5 道题已上线，C/C++ 秒级评测 → **[在线演示](http://122.51.84.172)**

### journal — header-only 的 C++11 同步/异步日志库

`C++11` `header-only` `CMake` `GitHub Actions` `MIT`

1093 行，零依赖，`#include "logs/yimingcode.h"` 即用。

- **双缓冲异步落盘**：生产者只做一次内存拷贝进 buffer，后台线程整块 swap 后批量 write，调用方不在 `write` 上阻塞
- **100 万条 64 字节记录**（i5-12400 / g++ 13.2 / `-O2`）：异步 **189 万条/秒**，同步 38 万条/秒，**约 5 倍**；4 线程异步吞吐接近线性
- 按大小 / 时间窗口滚动，可扩展 Sink（Stdout / File / RollBySize，自定义只需继承一个类），格式串可控 `%d %t %c %f:%l %p %m`
- GitHub Actions 每次 push 编译 example + extend 并跑回归脚本；异步写入异常不逃出工作线程，`errorCount()` 可查失败批次
- 边界写在 README 里：异步总耗时包含 worker 排空，不包含 `fsync` 持久性 → [journal-test](https://github.com/genius-pei/journal-test)

---

## 工作方式

两个项目都是 AI Agent 协同开发，但**验收标准由我先定死**：

1. 先写 `spec.md`，把每一条要求写成可测的验收项（比如「异步落盘不得丢记录」「停止后不再接受新数据」），不是写需求散文
2. AI 按阶段交付实现，每一轮 diff 我自己跑一遍 CI 再逐行读，不通过不进 `main`
3. 读不懂的地方去查标准 / 源码，不靠 AI 的自信——它写得比我快，但错得也比我自信

举个真实的例子：异步日志的 `stop()` 第一版直接 `join` 后台线程，缓冲区里还没落盘的数据会被丢掉。我改成置停止标志 → 排空队列 → 再 join，并补上失败批次计数和时序测试。这类「看起来对、边界上错」的地方是我审代码的重点。

---

## 技能

| | |
|---|---|
| 语言 | C / C++（C++11 / 17）、STL、数据结构与算法 |
| 系统 | Linux、fork/exec、信号量、条件变量、`setrlimit`、管道与 FD 管理 |
| 工具 | Git、CMake、GTest、Playwright、GitHub Actions |
| 数据 | MySQL 8（连接池、预处理、事务） |

---

## 写东西

C++ / Linux / MySQL 的踩坑记录，60+ 篇 → [blog.csdn.net/2401_85487070](https://blog.csdn.net/2401_85487070)

---

## 联系

📮 18808667810@163.com · 🐙 [@genius-pei](https://github.com/genius-pei)

<sub>目前：journal-test 已发布 v1.0.1（补齐 benchmark 数据），同时在读 fmt 的格式化层实现，准备从 issue 开始参与上游。</sub>
