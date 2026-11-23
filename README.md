# 裴奕名 · Yiming Pei

**C++ / Linux 系统编程** · 江汉大学 智能制造工程 2027 届 · 武汉

系统底层和跑在上面的应用都写。下面两个项目独立完成，从设计到上线。

---

## 项目

### MiniOJ — 仿 LeetCode 的轻量在线判题系统

`C++17` `cpp-httplib` `MySQL 8`

fork/exec 资源限制沙箱隔离用户提交，信号量控制并发评测，区分 AC / WA / TLE / CE / MLE / RE 六种判定。

- 5 道题，C/C++ 秒级评测 → **[在线演示](http://122.51.84.172)**
- 沙箱用 rlimit 限制 CPU 时间与内存，[待填：具体限制值和超时阈值]

### journal-test — 头文件 only 的 C++11 同步/异步日志库

`C++11` `header-only` `CMake` `GitHub Actions`

双缓冲异步落盘（调用方不阻塞在 write 上）、按大小/时间滚动、可扩展 Sink 架构，GitHub Actions 跑回归测试。

- [待填：benchmark 数据，例如 100 万条 64 字节记录，X M msg/s，p99 Y µs]
- [待填：对比同步模式快多少 / 是否做到零分配]

---

## 工作方式

两个项目的开发过程都用 AI Agent 协同（SPEC 驱动、分阶段交付），每轮产出由我逐行审过再合并。

> [待填：一句具体做法。比如 SPEC 写在哪、怎么验收、哪一次 AI 写错了我改成了什么]

---

## 技能

| | |
|---|---|
| 语言 | C / C++（C++11/17）、STL、数据结构 |
| 系统 | Linux、fork/exec、信号量、资源限制、内存管理 |
| 工具 | Git、CMake、GTest、Playwright、GitHub Actions |
| 数据 | MySQL 8 |

---

## 写东西

C++ / Linux / MySQL 的踩坑记录，60+ 篇 → [blog.csdn.net/2401_85487070](https://blog.csdn.net/2401_85487070)

---

## 联系

📮 18808667810@163.com · 🐙 [@genius-pei](https://github.com/genius-pei)

<sub>目前：给 journal-test 补 benchmark 与首个 release，同时在读 fmt 的格式化层实现。</sub>