# 电子商务管理系统

## 项目介绍

这是一个基于Python和MySQL开发的电子商务管理系统，提供客户管理、商品管理、订单管理等核心功能，适用于中小型电商企业的日常运营管理。

## 系统架构

- **前端**：使用Python Tkinter库开发图形用户界面
- **后端**：Python实现业务逻辑
- **数据库**：MySQL存储系统数据

## 目录结构

```
客户端code/
 ├── data/                         # 数据库相关文件
 │   ├── database/                 # 数据库结构和迁移
 │   │   ├── schema/               # 数据库结构文件
 │   │   └── migrations/           # 数据库迁移脚本
 │   └── config/                   # 配置文件
 │       ├── database.ini          # 数据库连接配置
 │       └── settings.json         # 应用设置
 ├── code/                         # 源代码和脚本
 │   ├── src/                      # 核心源代码
 │   │   ├── models/               # 数据模型
 │   │   ├── utils/                # 工具函数
 │   │   ├── gui/                  # 图形界面
 │   │   └── main.py               # 程序入口点
 │   ├── tests/                    # 测试文件
 │   │   ├── test_database.py      # 数据库操作测试
 │   │   └── test_models.py        # 模型测试
 │   ├── requirements.txt          # 项目依赖
 │   └── *.py                      # 各种功能脚本
 └── document/                     # 项目文档
     ├── README.md                 # 项目说明
     ├── docs/                     # 详细文档
     │   ├── ER_diagram.svg        # 实体关系图
     │   ├── requirements.md       # 需求分析
     │   ├── manual.md             # 用户手册
     │   └── data_generator_guide.md # 数据生成指南
     └── .gitignore                # Git忽略文件
```

## 主要文件功能说明

### 入口文件

- **src/main.py**: 程序主入口，负责初始化应用程序、设置异常处理和启动主循环。包含Windows DPI适配设置和全局异常捕获功能。

### 数据模型层 (src/models/)

- **database.py**: 实现数据库连接池管理，提供基础查询和更新操作，包含性能监控功能，支持事务处理和资源释放。
- **customer.py**: 实现客户数据模型，提供客户信息的查询、添加、更新和删除功能，支持客户数据的完整性验证。
- **product.py**: 实现商品数据模型，提供商品CRUD操作、库存管理、库存变更日志记录等功能。
- **order.py**: 实现订单数据模型，包含订单创建（含事务处理）、订单项管理和库存更新功能。
- **advanced_operations.py**: 提供跨表查询（如订单详情）和动态表管理（创建/删除表、添加/删除列）功能。

### 图形界面层 (src/gui/)

- **main_window.py**: 应用程序主窗口类，负责创建标签页控件、菜单栏和状态栏，集成各个功能模块的标签页。
- **customer_tab.py**: 客户管理标签页，提供客户搜索、添加、编辑、删除功能及客户订单统计。
- **product_tab.py**: 商品管理标签页，实现商品搜索、添加、编辑功能及商品统计。
- **order_tab.py**: 订单管理标签页，提供订单创建、查询、状态更新等功能。
- **order_items_tab.py**: 订单项管理标签页，支持订单项的查询和管理。
- **cart_tab.py**: 购物车管理标签页，支持购物车数据刷新和客户筛选。
- **inventory_logs_tab.py**: 库存日志管理标签页，提供库存变动记录查询和筛选。
- **table_management_tab.py**: 表管理标签页，支持数据库表的创建、删除和搜索。

### 工具函数 (src/utils/)

- **helpers.py**: 提供数据格式化、日期处理等辅助函数。
- **data_generator.py**: 实现测试数据生成器，包含客户、商品、订单数据的生成和清空功能。
- **bulk_data_generator.py**: 提供批量数据生成功能，支持生成大量客户、商品和订单数据，包含错误处理和进度显示。

### 测试文件 (tests/)

- **test_database.py**: 数据库操作测试类，测试数据库连接、查询、更新和事务操作。
- **test_models.py**: 数据模型测试类，测试客户、商品、订单等模型的功能。

### 脚本文件 (src/scripts/)

- **generate_large_customers.py**: 生成大量客户数据的脚本，用于性能测试。

### 其他文件

- **generate_test_data_for_new_tables.py**: 为新表生成测试数据的脚本。
- **config.ini**: 配置文件，包含数据库连接参数等配置信息。
- **transaction_example.py**: 事务操作示例文件，演示事务处理机制。
- **specific_transaction_example.py**: 具体事务操作示例，演示用户购买商品场景下的完整事务处理流程。

## 环境要求

- **操作系统**：Windows 11
- **Python版本**：Python 3.8或更高版本
- **数据库**：MySQL 5.7或更高版本
- **依赖库**：pymysql

## 安装指南

### 1. 安装Python

访问[Python官方网站](https://www.python.org/)下载并安装最新版本的Python。

### 2. 安装MySQL

访问[MySQL官方网站](https://dev.mysql.com/downloads/)下载并安装MySQL数据库。

### 3. 创建数据库

使用MySQL客户端工具创建一个名为`ecommerce_db`的数据库。

### 4. 初始化数据库

执行`database/schema/`目录下的SQL脚本初始化数据库：

```sql
-- 1. 创建表结构
SOURCE database/schema/01_tables_ddl.sql;

-- 2. 创建索引和外键
SOURCE database/schema/02_indexes_fk.sql;

-- 3. 插入示例数据（可选）
SOURCE database/schema/03_sample_data.sql;
```

### 5. 安装依赖包

```bash
pip install pymysql
```

### 6. 配置数据库连接

编辑`data/config/database.ini`文件，设置您的MySQL连接参数：

```ini
[database]
host = localhost
port = 3306
user = root
password = 您的MySQL密码
dbname = ecommerce_db
charset = utf8mb4
```

## 运行系统

在项目根目录下执行以下命令启动系统：

```bash
python code/src/main.py
```

## 关键文件功能介绍

### 核心源代码文件

#### 数据库连接和管理
- **src/models/database.py**：提供数据库连接池管理、SQL执行和性能监控功能，支持并发访问和事务处理，包含性能指标收集和记录慢查询功能。
- **src/main.py**：系统主入口文件，初始化各模块并启动GUI界面。

#### 业务模型
- **src/models/customer.py**：客户数据模型，实现客户信息的CRUD操作、搜索和统计功能。
- **src/models/product.py**：商品数据模型，处理商品信息管理、库存更新和商品分类查询。
- **src/models/order.py**：订单数据模型，提供订单创建、状态更新、查询和统计分析功能。

#### 工具和辅助函数
- **src/utils/config_manager.py**：配置文件管理，负责读取和解析数据库配置和系统设置。
- **src/utils/data_validator.py**：数据验证工具，确保输入数据的合法性和完整性。

### 测试和调试工具
- **test_db_connection.py**：数据库连接测试脚本，验证连接池配置和基础查询功能。
- **test_concurrent_access.py**：并发访问测试工具，模拟多用户并发操作，测试系统稳定性和性能。
- **tests/test_database.py**：数据库操作单元测试，验证各类SQL操作的正确性。

### 数据生成和管理工具
- **generate_test_data.py**：测试数据生成脚本，用于创建系统测试所需的示例数据。
- **generate_products_bulk.py**：批量商品数据生成工具，快速创建大量商品记录。
- **check_table_structure.py**：数据库表结构检查工具，验证数据库架构是否符合系统要求。

### 配置文件
- **data/config/database.ini**：数据库连接配置文件，包含主机、端口、用户名等连接参数。
- **data/config/settings.json**：系统设置配置文件，包含界面风格、日志级别等系统参数。

## 系统功能

### 客户管理
- 添加、查看、编辑和删除客户信息
- 搜索和筛选客户
- 客户统计分析

### 商品管理
- 添加、查看、编辑和删除商品信息
- 管理商品库存
- 搜索和筛选商品
- 商品统计分析

### 订单管理
- 查看和搜索订单
- 更新订单状态
- 取消订单
- 订单统计分析

### 高级数据操作
- 跨表查询（JOIN操作）
- 销售数据分析
- 客户购买行为分析

### 动态表管理
- 查看数据库中所有表
- 创建新表
- 删除表
- 添加/删除表列
- 查看表数据

## 测试

运行项目中的测试用例，确保系统功能正常：

```bash
python -m unittest discover code/tests
```

## 文档

- **需求分析**：`document/docs/requirements.md`
- **用户手册**：`document/docs/manual.md`
- **实体关系图**：`document/docs/ER_diagram.svg`
- **数据生成指南**：`document/docs/data_generator_guide.md`

## 开发说明

### 代码规范
- 遵循PEP 8 Python代码风格指南
- 所有函数和类都应有清晰的文档字符串
- 使用有意义的变量和函数名

### 开发环境设置

1. 克隆项目仓库
2. 创建Python虚拟环境
3. 安装依赖包
4. 配置数据库连接
5. 运行测试确保环境正常

## 维护说明

- 定期备份数据库
- 定期清理日志文件
- 系统出现问题时，查看日志文件获取详细错误信息

## 版权信息

© 2025 电子商务管理系统. 保留所有权利.
