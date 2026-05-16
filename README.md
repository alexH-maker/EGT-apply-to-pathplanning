# EGT-MAPF: 基于进化博弈论的多智能体路径规划

## 项目简介

本项目实现了基于**进化博弈论 (Evolutionary Game Theory, EGT)** 的多智能体路径规划算法 (MAPF)，并提供了与传统 A* 算法的对比实验框架。

该方法参考论文: *Multi Agent Path Finding using Evolutionary Game Theory*

## 核心特性

- **MAPF-EGT 算法**: 基于策略进化和轨迹适应度更新的多智能体路径规划
- **MAPF-A* 基线**: 时间扩展 A* 优先级规划算法，用于性能对比
- **自定义网格环境**: 支持障碍物随机生成、目标集合、碰撞检测
- **可视化**: 训练过程可视化与轨迹动画回放
- **批量实验**: 支持多次运行统计与结果导出

## 项目结构

```
EGT_MAPF/
├── mapf_egt/                    # 核心算法包
│   ├── __init__.py              # 导出接口
│   ├── env.py                   # 网格环境 (MultiAgentGridEnv)
│   ├── egt.py                   # MAPF-EGT 训练器与可视化
│   └── mapf_astar.py            # MAPF-A* 基线对比算法
├── mapf_settings.py             # 全局实验配置
├── run_mapf_egt.py              # 单次训练入口 (含动画回放)
├── batch_run_mapf_egt.py        # 批量多次运行
├── run_compare.py               # EGT vs A* 对比实验
└── Multi Agent Path Finding using Evolutionary Game Theory.pdf  # 参考论文
```

## 环境依赖

- Python 3.7+
- NumPy
- Matplotlib

```bash
pip install numpy matplotlib
```

## 快速开始

### 1. 单次训练与回放

```bash
python run_mapf_egt.py
```

运行单次 EGT 训练，训练完成后自动播放轨迹动画。

### 2. 批量运行

```bash
python batch_run_mapf_egt.py --runs 5 --agents 12
```

参数说明:
- `--runs`: 运行次数
- `--agents`: 智能体数量

### 3. 算法对比

```bash
python run_compare.py
```

运行 EGT 与 A* 算法的对比实验，结果输出至 `mapf_compare.csv`。

## 实验配置

在 `mapf_settings.py` 中可以修改实验参数:

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `GRID_SIZE` | (100, 100) | 网格大小 |
| `NUM_AGENTS` | 5 | 智能体数量 |
| `NUM_GOALS` | 5 | 目标数量 |
| `OBSTACLE_DENSITY` | 0.06 | 障碍物密度 |
| `NUM_EPISODES` | 500 | 训练轮数 |
| `MAX_STEPS` | 2000 | 每轮最大步数 |
| `SEED` | 42 | 随机种子 |

## 实验指标

- 平均路径长度
- 总步数
- 期望最小障碍距离
- 策略更新次数
- 计算时间

## 输出文件

- `mapf_egt_figures/`: 轨迹图输出目录
- `mapf_egt_runs.csv`: 批量运行结果
- `mapf_compare.csv`: 算法对比结果

## 算法原理

### MAPF-EGT

1. **策略构建**: 为每个智能体构建基于局部观测的策略
2. **轨迹采样**: 根据当前策略采样路径
3. **适应度评估**: 基于路径长度和碰撞情况计算适应度
4. **策略更新**: 根据适应度对策略进行奖励或惩罚

### MAPF-A*

基于时间扩展图的优先级规划:
- 按优先级顺序为每个智能体规划路径
- 使用顶点预留和边预留避免碰撞

## License

MIT License
