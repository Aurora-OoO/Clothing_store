# 服装店进销存管理系统 · Demo 说明

本文档用于演示仓库中的 **服装店进销存管理系统**（Java Swing + MySQL）的基本情况、运行方式与核心功能。

## 一、项目简介

- **项目名称**：服装店进销存管理系统
- **技术栈**：Java SE（Swing 桌面界面）、JDBC、MySQL 8.0
- **开发工具**：Eclipse（工程文件为 `.project` / `.classpath`）
- **界面语言**：简体中文
- **入口类**：`com.mingrisoft.MainFrame`

系统面向服装门店的日常经营，覆盖 **进货、销售、库存、往来单位与人员** 等核心业务环节。

## 二、目录结构

```
Clothing_store/
├── README.md
├── demo.md                        # 本文档
├── 服装店进销存管理系统/
│   ├── src/                       # 源代码
│   │   ├── com/mingrisoft/
│   │   │   ├── MainFrame.java     # 主窗口（程序入口）
│   │   │   ├── DesktopPanel.java  # 桌面面板
│   │   │   ├── dao/               # 数据访问层与实体模型
│   │   │   └── iframe/            # 各业务功能面板
│   │   ├── keyListener/           # 输入校验监听器
│   │   └── res/icon/              # 界面图标资源
│   ├── lib/                       # mysql-connector-java-8.0.20.jar
│   ├── Database/db_jxcms.sql      # 数据库建库脚本
│   ├── backup/                    # 数据库备份 SQL
│   └── bin/                       # 编译输出
├── 用例图.vsdx
├── 类图.vsdx
├── 数据流图.vsdx
├── 人员管理图.vsdx
├── 成本估算.vsdx
└── 服装店进销管理系统甘特图·.vsdx
```

> 设计文档（用例图、类图、数据流图、甘特图等）以 Visio `.vsdx` 格式随仓库提供。

## 三、功能模块

| 模块 | 主要功能 | 对应代码位置 |
| --- | --- | --- |
| 登录 | 操作员登录、修改密码 | `login/`、`iframe/GengGaiMiMa.java` |
| 商品管理 | 商品信息查询、添加、修改、价格调整 | `iframe/ShangPinGuanLi.java`、`ShangPinChaXun.java`、`JiaGeTiaoZheng.java` |
| 进货管理 | 进货入库、进货退货 | `iframe/JinHuoTuiHuo.java`、`dao/model/TbRukuMain.java` |
| 销售管理 | 销售开单、销售退货、销售查询、销售排行 | `iframe/XiaoShouTuiHuo.java`、`XiaoShouChaXun.java`、`XiaoShouPaiHang.java` |
| 库存管理 | 库存盘点、库存查询 | `iframe/KuCunPanDian.java`、`dao/model/TbKucun.java` |
| 供应商管理 | 供应商添加、修改、查询 | `iframe/GysGuanLi.java`、`GongYingShangChaXun.java` |
| 客户管理 | 客户添加、修改、管理 | `iframe/KeHuGuanLi.java`、`keHuGuanLi/` |
| 人员管理 | 操作员管理、经办人设置 | `iframe/JsrGL.java`、`czyGl/` |
| 系统维护 | 数据备份与恢复 | `iframe/BackupAndRestore.java` |

## 四、数据库设计（核心表）

| 表名 | 说明 |
| --- | --- |
| `tb_spinfo` | 商品信息 |
| `tb_kucun` | 库存信息 |
| `tb_ruku_main` / `tb_ruku_detail` | 进货主表 / 明细表 |
| `tb_rkth_main` / `tb_rkth_detail` | 进货退货主表 / 明细表 |
| `tb_sell_main` / `tb_sell_detail` | 销售主表 / 明细表 |
| `tb_xsth_main` / `tb_xsth_detail` | 销售退货主表 / 明细表 |
| `tb_gysinfo` | 供应商信息 |
| `tb_khinfo` | 客户信息 |
| `tb_jsr` | 经办人信息 |

建库脚本位于 `服装店进销存管理系统/Database/db_jxcms.sql`。

## 五、运行步骤

1. **准备数据库**
   ```bash
   mysql -u root -p < "服装店进销存管理系统/Database/db_jxcms.sql"
   ```
   或使用 `backup/` 目录下的备份文件进行恢复。

2. **配置数据库连接**
   修改 `src/com/mingrisoft/dao/Dao.java` 中的 `dbUrl`、`dbUser`、`dbPwd` 等连接参数，使其匹配本地 MySQL 环境。

3. **导入工程**
   在 Eclipse 中通过 *File → Import → Existing Projects into Workspace* 导入 `服装店进销存管理系统` 目录，确认 `lib/mysql-connector-java-8.0.20.jar` 已加入构建路径。

4. **运行程序**
   运行 `com.mingrisoft.MainFrame` 的主方法，使用数据库中的操作员账号登录。

## 六、演示流程建议

1. 登录系统，进入主界面。
2. 在 **商品管理** 中新增一件商品并设置售价。
3. 在 **进货管理** 中录入进货单，观察库存增加。
4. 在 **销售管理** 中开销售单，观察库存扣减。
5. 在 **库存盘点** 中核对库存数量。
6. 在 **销售排行** 中查看销售统计。
7. 在 **系统维护** 中执行一次数据备份。

## 七、说明

- 本仓库为教学 / 课程设计性质的项目，代码与文档配套提供。
- 数据库连接信息请勿提交到版本库，建议在本地修改后使用占位符代替。
